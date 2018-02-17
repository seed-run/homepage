---
layout: docs
title: Viewing Metrics
---

[Seed](/) pulls together CloudWatch metrics to give you an overview of your deployments. You can view the metrics for your Lambda and API Gateway endpoints.

### Lambda Metrics

To view the Lambda metrics for a stage, simply head over to the stage and click on **View Deployment**.

![View Deployment](/assets/docs/viewing-metrics/view-deployment.png)

Here Seed gives you a clear overview of the resources that have been deployed.

![Deployment Info](/assets/docs/viewing-metrics/deployment-info.png)

And hit **Metrics** for the Lambda you are interested in.

![Lambda Metrics](/assets/docs/viewing-metrics/lambda-metrics.png)

For Lambda, Seed shows you the following metrics:

1. **Invocation Count**

   This is the number of times the Lambda has been invoked.

2. **Duration**

   This is the average time (in ms) it took to execute the Lambda.

3. **Error Count**

   This is the number of times the Lambda generated an error.

To get a better sense of how the metrics are calculated over the various timespans, read the section below on [Timespan of Graphs](#timespan-of-graphs);

### API Gateway Metrics

To view the API Gateway metrics for a stage, click on **Metrics** on the API Gateway portion of your resources.

![Deployment Info](/assets/docs/viewing-metrics/deployment-info.png)

The API Gateway metrics have a bit more info than the Lambda metrics.

![API Gateway Metrics](/assets/docs/viewing-metrics/api-gateway-metrics.png)

Here are the metrics for API Gateway:

1. **Request Count**

   This is the number of requests made to API Gateway.

2. **4xx Errors**

   This is the number of 4xx response errors generated for the requests.

3. **5xx Errors**

   This is the number of 5xx response errors generated for the requests.

4. **Latency**

   This is the average time (in ms) it took to make the entire request.

5. **Integration Latency**

   This is the average time (in ms) it took to make the Lambda part of the request.

You might notice in some cases that the **Integration Latency** is larger that the **Latency** (even though the Latency should be the total request time). This is because **OPTIONS** requests do not hit your Lambdas and have an Integration Latency of 0. And as a result it brings down the average for the Integration Latency of requests.

### Timespan of Graphs

You can view the various metrics over the following timespans and each point is the data collected for the given amount of time.

| Label | Timespan   | Each Point |
|-------|------------|------------|
| Live  | 60 minutes | 1 minute   |
| 24H   | 24 hours   | 30 minutes |
| 1WK   | 1 week     | 3 hours    |
| 1MO   | 1 month    | 1 day      |
|-------|------------|------------|

So for example, in the 24H setting (24 hours); the total number of points are displayed over the span of 24 hours. While each point on the graph represents the amount of the data collected over the span of 30 minutes. In the case of a count, this is the total number over the span of 30 minutes. And for a duration type metric, it is the average of the points collected over 30 minutes.
