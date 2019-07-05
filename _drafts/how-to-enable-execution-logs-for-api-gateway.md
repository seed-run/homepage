---
layout: post
title: How to enable execution logs for API Gateway?
image: assets/social-cards/enable-execution-logs.png
description: In this post we'll look at how to enable execution logs in API Gateway by creating an IAM role to allow API Gateway to log to CloudWatch. We'll also look at how to view API Gateway execution logs in the CloudWatch console by using the log groups and log streams that are created. 
categories: tips
author: jack
---

In this post we are going to look at how to enable and use execution logs for API Gateway in CloudWatch.

Just a quick recap, there are two ways of logging API Gateway:

- Execution logs: Logs with detailed information as API Gateway goes through each step of processing the request. Useful for tracing individual requests. Can generate lots of log data, resulting in a large CloudWatch bill.
- Access logs: Logs of who has accessed your API. Each request generates a single entry in the logs, similar to NGINX logs. Useful for sending to an analytics tool to gather metrics.

Let's start by looking at how to enable execution logs.


### Enabling API Gateway execution logs

This is a two step process. First, we need to create an IAM role that allows API Gateway to write logs to CloudWatch. Then we need to turn on logging for our API Gateway project.

Start by logging into your [AWS Console](https://console.aws.amazon.com/) and select IAM from the list of services.

![Select IAM from list of AWS services](https://d33wubrfki0l68.cloudfront.net/07bc0503a7d837f6f3c284b498d225b58dac783f/aa9a2/assets/logging/select-iam-service.png)

Click **Roles** on the left menu.

![Select IAM Roles from left menu](https://d33wubrfki0l68.cloudfront.net/fbc6e501d1350a7177a00cf593d0749d14c6e326/b3770/assets/logging/select-iam-roles.png)

Click **Create role**.

![Select Create IAM Role](https://d33wubrfki0l68.cloudfront.net/8857bba78f8b2c909a80d8989788fc254d433c3f/267bd/assets/logging/select-create-iam-role.png)

Under **AWS service**, select **API Gateway**.

![Select API Gateway from AWS services](https://d33wubrfki0l68.cloudfront.net/6f777a1046a80b7b200b64b1e971330191e7f3fe/49e68/assets/logging/select-api-gateway-iam-role.png)

Click **Next: Permissions**.

![Click Next: Permissions](https://d33wubrfki0l68.cloudfront.net/f29c9b06f7b09832dd25f788fac7cebcfc94a866/164f3/assets/logging/select-iam-role-attach-permissions.png)

Click **Next: Review**.

![Click Next: Review](https://d33wubrfki0l68.cloudfront.net/ebbba71519556778ac91a19fcc0c40421084c7d8/a8471/assets/logging/select-review-iam-role.png)

Enter a **Role name** and click **Create role**. In our case, we call our role `APIGatewayCloudWatchLogs`.

![Enter a role name and create role](https://d33wubrfki0l68.cloudfront.net/d7cee9dcd3dc60673426940c059c9f1fe1ff6698/a7390/assets/logging/fill-in-iam-role-info.png)

Click on the role we just created.

![Click on new role](https://d33wubrfki0l68.cloudfront.net/8c66c2eeacb2a0e946276671988746a0f1ad23e8/66076/assets/logging/select-created-api-gateway-iam-role.png)

Make a note of the **Role ARN**. We'll be needing this soon.

![Copy Role ARN](https://d33wubrfki0l68.cloudfront.net/f308acfc467e0e31b2543785e62ee37170289bb9/1d8c5/assets/logging/iam-role-arn.png)

Now that we've created an IAM role, let’s turn on logging for our API Gateway project.

Go back to your [AWS Console](https://console.aws.amazon.com/) and select API Gateway from the list of services.

![Select API Gateway from list](https://d33wubrfki0l68.cloudfront.net/43d4ff3647df55040a6b5e34df09aa3bdd45a059/9bc20/assets/logging/select-api-gateway-service.png)

Click on **Settings** in the left panel.

![Click on API Gateway settings](https://d33wubrfki0l68.cloudfront.net/e6fc71499ce75b914437ee6cba01b236c32569c8/2bc8b/assets/logging/select-api-gateway-settings.png)

Enter the **ARN** of the IAM role we just created in the **CloudWatch log role ARN** field and hit **Save**.

![Enter IAM Role ARN and save](https://d33wubrfki0l68.cloudfront.net/9915ca6535e00478ea77b6bce1c8a136b9ddb4b0/af784/assets/logging/fill-in-api-gateway-cloudwatch-info.png)

Select your API project from the left panel, click **Stages**, then pick the stage you want to enable logging for. For our API, we deployed it to the prod stage.

![Select API Gateway project and stage](https://d33wubrfki0l68.cloudfront.net/53d1bb6c9e74b004b5649e277f6de98ce6359711/a5705/assets/logging/select-api-gateway-stage.png)

In the Logs tab:

- Check **Enable CloudWatch Logs**.
- Select **INFO** for **Log level** to log every request.
- Check **Log full requests/responses data** to include entire request and response body in the log.
- Check **Enable Detailed CloudWatch Metrics** to track latencies and errors in CloudWatch metrics.

![Enable Execution Logging and CloudWatch Metrics](https://d33wubrfki0l68.cloudfront.net/dc97716952073a07ec44dcb9cd7f7745d50279f3/12709/assets/logging/fill-in-api-gateway-logging-info.png)

Scroll to the bottom of the page and click **Save changes**. Now our API Gateway requests should be logged via CloudWatch.


### Viewing API Gateway execution logs

CloudWatch groups log entries into Log Groups and then further into Log Streams. Log Groups and Log Streams can mean different things for different AWS services. For API Gateway, when logging is first enabled in an API project’s stage, API Gateway creates 1 log group for the stage, and 300 log streams in the group ready to store log entries. API Gateway picks one of these streams when there is an incoming request.

To view API Gateway logs, log in to your AWS Console and select CloudWatch from the list of services.

![Select CloudWatch service](https://d33wubrfki0l68.cloudfront.net/eff00ffdc2b2680ebeeac8c09db64c1db8431d29/e69b0/assets/logging/select-cloudwatch-service.png)

Select **Logs** from the left panel.

![Select CloudWatch logs](https://d33wubrfki0l68.cloudfront.net/93be646196ce32a9e020f95e53a2a5d62c4a4df9/bfcbc/assets/logging/select-cloudwatch-logs.png)

Select the log group that starts with `API-Gateway-Execution-Logs_` followed by the API Gateway id.

![Select log group with API Gateway id](https://d33wubrfki0l68.cloudfront.net/8d0374141cef8e64b57ef4380a9bbc70c4bfcf35/1cc29/assets/logging/select-cloudwatch-api-gateway-log-group.png)

You should see 300 log streams ordered by the last event time. This is the last time a request was recorded. Click on the first stream.

![Select first log stream from group](https://d33wubrfki0l68.cloudfront.net/94795fb484a734fd43be762ce15ec2ad432dd55e/0f37a/assets/logging/select-cloudwatch-api-gateway-log-stream.png)

This shows you one log entry for each API request. Expand a row, the log data should reflect the format you had previously defined.

![Select log row from API Gateway request](https://d33wubrfki0l68.cloudfront.net/22d1a2381b583cf7601b0f198394b2a3c359f7b1/f2bc0/assets/logging/cloudwatch-api-gateway-log-entries.png)

Note that, two consecutive groups of logs are not necessarily two consecutive requests in real time. This is because there might be other requests that are processed in between these two that were picked up by one of the other log streams.

#### Summary

This post should give you a good idea of how to enable execution logs for your API Gateway project and also how to view them from the CloudWatch console.
