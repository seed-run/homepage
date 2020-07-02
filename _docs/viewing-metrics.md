---
layout: docs
title: Viewing Metrics
---

[Seed](/) pulls together CloudWatch Metrics to give you an overview of your Lambda and API metrics. This includes the number of requests, and latency of your Lambda function or API endpoint over time. Viewing these metrics gives you a view of how your Serverless app is performing and you can use it to debug specific issues.

A couple of quick notes about the metrics viewer in Seed:

- Seed internally uses CloudWatch Metrics for this.
- This means that you get unlimited data retention!
- However, AWS will charge you small amount based on your region. It's roughly $0.01 per 1,000 metrics queried. Make sure to check the [CloudWatch Metrics pricing](https://aws.amazon.com/cloudwatch/pricing/) for your region.
- We also need a couple of additional permissions to connect to CloudWatch in your account. More on this below.

### Lambda Metrics

To view the Lambda metrics for a stage, simply select the stage.

![Select stage](/assets/docs/viewing-metrics/select-stage.png)

Click **View Resources** for the service you are looking for and navigate to the **Metrics** for the Lambda function.

![Stage view resources](/assets/docs/viewing-metrics/stage-view-resources.png)

This gives you a live look at the last **1 hour** of metrics.

![Lambda Metrics Live](/assets/docs/viewing-metrics/lambda-metrics-live.png)

You can easily view the metrics for a different period of time. The time field can take a specific time, range, timestamp, or even a different timezone.

![Lambda Logs change duration filter](/assets/docs/viewing-metrics/lambda-metrics-change-duration-filter.png)

For Lambda, Seed shows you the following metrics:

1. **Invocation Count**

   This is the number of times the Lambda has been invoked.

2. **Duration**

   This is the average, P90, P95, and P99 time (in ms) it took to execute the Lambda.

### API Gateway Metrics

To view the API Gateway metrics for a stage, click on **Metrics** for the API endpoint. Or you can use the search field just as above.

![Stage API Metrics](/assets/docs/viewing-metrics/stage-api-metrics.png)

Similar to the Lambda metrics, you get a live view of the last hour of metrics.

![API Metrics Live](/assets/docs/viewing-metrics/api-metrics-live.png)

You can view the following API metrics here:

1. **Request Count**

   This is the number of requests made to API Gateway.

2. **Latency**

   This is the average, P90, P95, and P99 time (in ms) it took to respond to a request.

### Additional IAM Permissions

To connect to CloudWatch in your AWS account, Seed needs the following set of additional permissions.
  
``` json
{
  "PolicyName": "MonitorMetrics",
  "PolicyDocument": {
    "Version": "2012-10-17",
    "Statement": [
      {
        "Effect": "Allow",
        "Action": [
          "apigateway:GET",
          "cloudwatch:GetMetricData"
        ],
        "Resource": "*"
      }
    ]
  }
}
```

The metrics viewer in Seed is designed to work with your development workflow by helping you quickly debug any issues with your deployed apps.
