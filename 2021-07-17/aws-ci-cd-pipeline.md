
# AWS Continuous Deployment

The CDK team at AWS does promise (highlevel tooling)[https://docs.aws.amazon.com/cdk/latest/guide/cdk_pipeline.html] in the near future. 
The (CDKPipeline construct)[https://docs.aws.amazon.com/cdk/api/latest/docs/@aws-cdk_pipelines.CdkPipeline.html] is missing some key features.
The new API has merged earlier this week and should be available in the next release of the (@aws/pipelines)[https://github.com/aws/aws-cdk/tree/master/packages/%40aws-cdk/pipelines] package.
The modern API comes with the (CodePipeline construct)[https://docs.aws.amazon.com/cdk/api/latest/docs/@aws-cdk_pipelines.CodePipeline.html] 
which supports in-built (self-mutation)[https://github.com/aws/aws-cdk/tree/master/packages/%40aws-cdk/pipelines#working-on-the-pipeline] 
and (multiple inputs)[https://github.com/aws/aws-cdk/tree/master/packages/%40aws-cdk/pipelines#additional-inputs].
While we await an official release let's explore the primitive (codepipeline.Pipeline construct)[https://docs.aws.amazon.com/cdk/api/latest/docs/@aws-cdk_aws-codepipeline.Pipeline.html].

### An Application Stack

The (lambda package)[https://github.com/npxcomplete/aws-request-logger-lambda]


