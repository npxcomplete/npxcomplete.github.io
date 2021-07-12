
# Payment Basics

I was recently asked by an acquaintance to lend my expertise as a software engineer to their current struggle with website payment systems.
Wanting to be a helpful soul, but having no explicit knowledge of stripe, paypal, aws payments, or gpay I said I'd look into it and get back to them.
What followed is this blog entry where I attempt to show how I would approach learning about one of these systems based on what little I know already, and a desire to at some point sell other humans an online service.

### The Basic Model

I have chosen to play with paypal's API first because I like their checkout experience as a customer. 
However, the basic model will be similar across all solutions. 
Note that I'll describe the service to service model.
Paypal's magic button skips a step or two.

1) A customer builds a shopping cart.
2) The website offers a pay with paypal option.
3) The customers browser sends the "checkout with paypal" request to the server.
4) The server submits the request to paypal and paypal returns four URLs. 
```json
{
  "id": "5O190127TN364715T",
  "status": "CREATED",
  "links": [
    {
      "href": "https://api-m.paypal.com/v2/checkout/orders/5O190127TN364715T",
      "rel": "self",
      "method": "GET"
    },
    {
      "href": "https://www.paypal.com/checkoutnow?token=5O190127TN364715T",
      "rel": "approve",
      "method": "GET"
    },
    {
      "href": "https://api-m.paypal.com/v2/checkout/orders/5O190127TN364715T",
      "rel": "update",
      "method": "PATCH"
    },
    {
      "href": "https://api-m.paypal.com/v2/checkout/orders/5O190127TN364715T/capture",
      "rel": "capture",
      "method": "POST"
    }
  ]
}
```
The two URLs we're immediately interested in are "approve" and "capture".

5) The server sends "approve" back to the customer's browser and opens the link in a new tab / window.
6) The customer logs in and approves the checkout on paypals site.
7) Paypal calls a webhook / sends an event to the server saying "yes, the payment was approved"
8) The server calls "capture" to confirm the payment and recieves success response.
9) The server marks the order shippable.

### Creating an Integrated Debug Environment

It is really useful to have a request logger when dealing with webhook based APIs. 
To begin, before doing anything else, I setup an AWS Lambda function that takes whatever it is given and logs that request.
I think go is pretty good for webservices.
Even if you don't know golang, if you know some other imperative programming language, you should be able to grok the guts of this Lambda:
```golang
package main

import (
	"context"
	"encoding/json"
	"fmt"
	"github.com/aws/aws-lambda-go/events"
	"github.com/aws/aws-lambda-go/lambda"
)

func main() {
	lambda.Start(func(ctx context.Context, event interface{}) (resp interface{}, err error) {
		// all events arrive as JSON objects
		bs, err := json.Marshal(event)
		if err != nil {
			fmt.Println("Error serializing json event.")
			return
		}

		// The entire purpose of this lambda func
		fmt.Println(string(bs))

		// play nice with api gateway / http clients
		err = nil
		resp = events.APIGatewayProxyResponse{
			StatusCode:        200,
			Body:              "{\"goodbye\": \"world\"}",
		}
		return
	})
}
```
This is all well and good, but now that I have this code I need to put it "into production", which is where my software engineering brain takes over.
Does this little function deserve the attention of a full deployment pipeline?...Noooooooooooooooooooooo.
However, if we build anything remotely complicated later we'll want the convenience of a full CDK pipeline.
Therefore, it makes sense to figure out the pipeline tooling with this little toy where the complexity of the application itself doesn't get in the way of getting the pipeline working.




