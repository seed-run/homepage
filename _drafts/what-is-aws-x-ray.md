# What is AWS X-Ray?

AWS X-Ray is a service that records and visualize requests made by your application. It provides an end-to-end view of requests as they travel through your application, and shows a map of your application's underlying components.

TL,DR; If you want to enable X-Ray for your Serverless app and learn how to ready a trace, here is an article that help you to do that.


### Why should I use X-Ray for my Serverless app?

Take this Lambda function for example. Imaging it is invoked by an API Gateway endpoint, and it publishes a SNS message and makes 2 queries to DynamoDB, a fairly simple and common use case.


```
const aws = require('aws-sdk');
const dynamodb = new AWS.DynamoDB.DocumentClient();
const sns = new AWS.SNS();

export async function main(event, context) {
  await sns.publish({ ... }).promise();
  await dynamodb.put({ ... }).promise();
  await dynamodb.put({ ... }).promise();
}
```

Now, a user makes an API call and gets a 500 HTTP response, there can be many point of failures:
 1. was the API itself poorly formatted?
 2. did API Gateway invoked the Lambda function successfully?
 3. did the Lambda function experienced a cold start and caused the request timeout?
 4. did SNS fail to publish the message?
 5. did DynamoDB fail? If so, the first query or the second?

You have to rely on a per-service or per-resource process to track the request down as it travels across various services. This makes it difficult to correlate the various pieces of data and create an end-to-end picture of a request from the time it originates at the end-user or service to when a response is returned by your application.


### What can X-Ray do?

X-Ray can record a thorough chronological trace for your API requests including starting from API Gateway receiving the request all the way to sending a response back to the user. A trace looks like:

[ SCREEN SHOT OF TRACE ]

It shows:
- when the request is received by API Gateway, and how long it took
- when the request is received by Lambda
- how long it took SNS to publish the request
- how long each DynamoDB query took and the type of the query


### How does it work?

When you app receives an HTTP request, the first supported service that handles the request adds a trace ID to the header. In our case, it is the API Gateway. It then propagates the trace ID downstream to Lambda, and in turn to SNS and DynamoDB. This way, a trace ID travels the entire path of a request and tracks the latency, disposition, and other request data. In the end, all information with the same trace ID is then formatted and presented in the chronological order you see by X-Ray.


### How much does it cost?

X-Ray comes with a [free tier](https://aws.amazon.com/xray/pricing/). Beyond that you are charged by the amount of requests that are traced.

You can control how much you want to trace via sample rate. By default, the X-Ray SDK records the first request each second, and five percent of any additional requests. You can configure X-Ray to modify the default sampling rule and configure additional rules that apply sampling based on properties of the service or request.

For example, you might want to disable sampling and trace all requests for calls that modify state or handle user accounts or transactions. For high-volume read-only calls, like background polling, health checks, or connection maintenance, you can sample at a low rate and still get enough data to see any issues that arise.

