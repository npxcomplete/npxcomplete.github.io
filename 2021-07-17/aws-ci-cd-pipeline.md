
# AWS Continuous Deployment

The CDK team at AWS does promise [highlevel tooling](https://docs.aws.amazon.com/cdk/latest/guide/cdk_pipeline.html) in the near future. 
The [CDKPipeline construct](https://docs.aws.amazon.com/cdk/api/latest/docs/@aws-cdk_pipelines.CdkPipeline.html) is missing some key features.
The new API has merged earlier this week and should be available in the next release of the [@aws/pipelines](https://github.com/aws/aws-cdk/tree/master/packages/%40aws-cdk/pipelines) package.
The modern API comes with the [CodePipeline construct](https://docs.aws.amazon.com/cdk/api/latest/docs/@aws-cdk_pipelines.CodePipeline.html) 
which supports in-built [self-mutation](https://github.com/aws/aws-cdk/tree/master/packages/%40aws-cdk/pipelines#working-on-the-pipeline) 
and [multiple inputs](https://github.com/aws/aws-cdk/tree/master/packages/%40aws-cdk/pipelines#additional-inputs).
While we await an official release let's explore the primitive [codepipeline.Pipeline construct](https://docs.aws.amazon.com/cdk/api/latest/docs/@aws-cdk_aws-codepipeline.Pipeline.html).

### An Application Stack

The [lambda package](https://github.com/npxcomplete/aws-request-logger-lambda) produces an executable named `main`. The naming is a required convention of the golang lambda runtime.
The corrosponding [pipeline package](https://github.com/npxcomplete/aws-request-logger-pipeline) produces two stacks:
* PipelinesStack
* LambdaStack

The lambda stack deploys our lambda function to an API gateway and outputs the API's URL:
```typescript
import * as cdk from '@aws-cdk/core';
import * as codedeploy from '@aws-cdk/aws-codedeploy';
import * as lambda from '@aws-cdk/aws-lambda';
import * as apigateway from '@aws-cdk/aws-apigateway';
import * as cwlogs from '@aws-cdk/aws-logs';

export class RequestLoggerStack extends cdk.Stack {
    public readonly codeArtifact: lambda.CfnParametersCode
    public readonly apiUrl: cdk.CfnOutput;

    constructor(scope: cdk.Construct, id: string, props?: cdk.StackProps) {
        super(scope, id, props);

        this.codeArtifact = lambda.Code.fromCfnParameters();

        const fn = new lambda.Function(this, 'ApplicationFunction', {
            runtime: lambda.Runtime.GO_1_X,
            handler: 'main',
            code: this.codeArtifact,
            functionName: 'request-logger',
        });
        
        const alias = new lambda.Alias(this, 'LambdaAlias', {
            aliasName: 'Prod',
            version: fn.currentVersion,
        });
        
        const deploymentGroup = new codedeploy.LambdaDeploymentGroup(this, 'DeploymentGroup', {
            alias: alias,
            deploymentConfig: codedeploy.LambdaDeploymentConfig.LINEAR_10PERCENT_EVERY_1MINUTE,
        });


        const logGroup = new cwlogs.LogGroup(this, "ApiGatewayAccessLogs");
        const api = new apigateway.LambdaRestApi(this, 'FuncGateway', {
            handler: fn,
            cloudWatchRole: true,
            deployOptions: {
                accessLogDestination: new apigateway.LogGroupLogDestination(logGroup),
                accessLogFormat: apigateway.AccessLogFormat.jsonWithStandardFields(),
                tracingEnabled: true,
            },
        });

        new cdk.CfnOutput(this, 'lambdaArn', {
            exportName: 'lambdaARN',
            value: fn.functionArn,
        })

        this.apiUrl = new cdk.CfnOutput(this, 'lambdaUrl', {
            exportName: 'lambdaUrl',
            value: api.url,
        })
    }
}
```

The pipeline stack is a bit more involved. It creates two pipelines, the first being our self-mutation loop:
```typescript
    const pipeline = new codepipeline.Pipeline(stack, 'Pipeline', {
        pipelineName: "PipelineMutation",
    });

    pipeline.addStage({
        stageName: 'Source',
        actions: [sourceCdkPipelineCode],
    })

    pipeline.addStage({
        stageName: 'Build',
        actions: [compileAndSynthCdk],
    })

    pipeline.addStage({
        stageName: 'Deploy',
        actions: [deployPipelines],
    })
```
The second performs the deploy of the lambda function:
```typescript
    const pipeline = new codepipeline.Pipeline(stack, 'RequestLoggerPipeline', {
        pipelineName: "RequestLoggerPipeline"
    });

    pipeline.addStage({
        stageName: 'Source',
        actions: [sourceCdkPipelineCode, sourceRequestLoggerCode],
    })

    pipeline.addStage({
        stageName: 'Build',
        actions: [compileAndSynthCDK, compileRequestLogger],
    })

    pipeline.addStage({
        stageName: 'Deploy',
        actions: [updateRequestLoggerStack],
    })

    pipeline.addStage({
        stageName: 'Verify',
        actions: [verifyLambda],
    });
```
Note the additional verify step. Verify is dependent on the API URL that the lambda stack outputs. This creates a cyclic dependency between the two stacks that needs to be broken during the initial deployment. Breaking the cycle is as simple as commenting out the argument in the verify build script:
```typescript
function createLambdaVerify(url: CfnOutput): codebuild.PipelineProjectProps {
    return {
        buildSpec: codebuild.BuildSpec.fromObject({
            version: '0.2',
            phases: {
                install: {
                    commands: ['bash ./bin/install'],
                },
                build: {
                    // Initial deploy will fail, requiring this import to be hidden, due to
                    // the circular dependency it creates.
                    commands: `bash ./bin/verify` # HERE # ${Fn.importValue(url.exportName!)}`,
                },
            },
            artifacts: {
                'base-directory': 'build',
                files: [],
            },
        }),
        environment: {
            buildImage: codebuild.LinuxBuildImage.STANDARD_5_0,
        },
    };
}
```
After deploying the cycle-broken version from your local host, CodePipelines will automatically attempt a deploy of lambda that will fail at the verify step. You can manually trigger a redeploy of the pipeline from source in AWS console. This will reinstate the cycle and when the lambda deployment reaches verify again it should now have the URL available and pass the check.
