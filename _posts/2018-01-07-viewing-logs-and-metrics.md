---
layout: post
title: Viewing Logs and Metrics
categories: news
author: frank
---

Seed now displays logs and metrics for your deployments. You can also enable API Gateway access logs. This allows you to monitor your deployments right from the Seed console!

![Lambda Metrics](/assets/blog/viewing-logs-and-metrics/lambda-metrics.png)

By heading over to the deployment page you can see a list of all the Lambdas and API Gateway endpoints. And you can click to view the metrics and logs for them. The metrics include the CloudWatch metrics for Lambda and API Gateway. And for the logs, you can view the Lambda logs and API Gateway access logs.

![Lambda Logs](/assets/blog/viewing-logs-and-metrics/lambda-logs.png)

[Viewing logs for your Serverless AWS application](https://serverless-stack.com/chapters/api-gateway-and-lambda-logs.html) was fairly cumbersome in the past. And the [`serverless logs` command](https://serverless.com/framework/docs/providers/aws/cli-reference/logs/) is usually only available to a single developer on your team. By pulling in the logs and metrics live for your deployments, Seed allows you to quickly track down any deployment issues. This greatly streamlines the CI/CD pipeline for your Serverless projects and allows the developers on your team to collaborate better.

You can read more about [viewing logs]({% link _docs/viewing-logs.md %}) and [metrics]({% link _docs/viewing-metrics.md %}) in our docs.
