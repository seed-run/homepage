---
layout: post
title: How to enable execution logs for API Gateway
image: assets/social-cards/enable-execution-logs.png
description: In this post we'll look at how to enable execution logs in API Gateway by creating an IAM role to allow API Gateway to log to CloudWatch. We'll also look at how to view API Gateway execution logs in the CloudWatch console by using the log groups and log streams that are created. 
categories: tips
author: jack
---

In this post we are going to look at how to enable and use execution logs for API Gateway in CloudWatch.

Just a quick recap, there are two ways of logging API Gateway:

- Execution logs: Logs with detailed information as API Gateway goes through each step of processing the request. Useful for tracing individual requests. Can generate lots of log data, resulting in a large CloudWatch bill.
- Access logs: Logs of who has accessed your API. Each request generates a single entry in the logs, similar to NGINX logs. Useful for sending to an analytics tool to gather metrics.

We have a detailed post looking at [the differences between execution logs and access logs here]({% link _posts/2019-07-05-whats-the-difference-between-access-logs-and-execution-logs-in-api-gateway.md %}).

Let's start by looking at how to enable execution logs.


### Enabling API Gateway execution logs

This is a two step process. First, we need to create an IAM role that allows API Gateway to write logs to CloudWatch. Then we need to turn on logging for our API Gateway project.

Start by logging into your [AWS Console](https://console.aws.amazon.com/) and select IAM from the list of services.

![Select IAM from list of AWS services](/assets/blog/how-to-enable-execution-logs-for-api-gateway/select-iam-from-list-of-aws-services.png)

Click **Roles** on the left menu.

![Select IAM Roles from left menu](/assets/blog/how-to-enable-execution-logs-for-api-gateway/select-iam-roles-from-left-menu.png)

Click **Create role**.

![Select Create IAM Role](/assets/blog/how-to-enable-execution-logs-for-api-gateway/select-create-iam-role.png)

Under **AWS service**, select **API Gateway**.

![Select API Gateway from AWS services](/assets/blog/how-to-enable-execution-logs-for-api-gateway/select-api-gateway-from-aws-services.png)

Click **Next: Permissions**.

![Click Next: Permissions](/assets/blog/how-to-enable-execution-logs-for-api-gateway/click-next-permissions.png)

Click **Next: Review**.

![Click Next: Review](/assets/blog/how-to-enable-execution-logs-for-api-gateway/click-next-review.png)

Enter a **Role name** and click **Create role**. In our case, we call our role `APIGatewayCloudWatchLogs`.

![Enter a role name and create role](/assets/blog/how-to-enable-execution-logs-for-api-gateway/enter-a-role-name-and-create-role.png)

Click on the role we just created.

![Click on new role](/assets/blog/how-to-enable-execution-logs-for-api-gateway/click-on-new-role.png)

Make a note of the **Role ARN**. We'll be needing this soon.

![Copy Role ARN](/assets/blog/how-to-enable-execution-logs-for-api-gateway/copy-role-arn.png)

Now that we've created an IAM role, let’s turn on logging for our API Gateway project.

Go back to your [AWS Console](https://console.aws.amazon.com/) and select API Gateway from the list of services.

![Select API Gateway from list](/assets/blog/how-to-enable-execution-logs-for-api-gateway/select-api-gateway-from-list.png)

Click on **Settings** in the left panel.

![Click on API Gateway settings](/assets/blog/how-to-enable-execution-logs-for-api-gateway/click-on-api-gateway-settings.png)

Enter the **ARN** of the IAM role we just created in the **CloudWatch log role ARN** field and hit **Save**.

![Enter IAM Role ARN and save](/assets/blog/how-to-enable-execution-logs-for-api-gateway/enter-iam-role-arn-and-save.png)

Select your API project from the left panel, click **Stages**, then pick the stage you want to enable logging for. For our API, we deployed it to the prod stage.

![Select API Gateway project and stage](/assets/blog/how-to-enable-execution-logs-for-api-gateway/select-api-gateway-project-and-stage.png)

In the Logs tab:

- Check **Enable CloudWatch Logs**.
- Select **INFO** for **Log level** to log every request.
- Check **Log full requests/responses data** to include entire request and response body in the log.
- Check **Enable Detailed CloudWatch Metrics** to track latencies and errors in CloudWatch metrics.

![Enable Execution Logging and CloudWatch Metrics](/assets/blog/how-to-enable-execution-logs-for-api-gateway/enable-execution-logging-and-cloudwatch-metrics.png)

Scroll to the bottom of the page and click **Save changes**. Now our API Gateway requests should be logged via CloudWatch.


### Viewing API Gateway execution logs

CloudWatch groups log entries into Log Groups and then further into Log Streams. Log Groups and Log Streams can mean different things for different AWS services. For API Gateway, when logging is first enabled in an API project’s stage, API Gateway creates 1 log group for the stage, and 300 log streams in the group ready to store log entries. API Gateway picks one of these streams when there is an incoming request.

To view API Gateway logs, log in to your AWS Console and select CloudWatch from the list of services.

![Select CloudWatch service](/assets/blog/how-to-enable-execution-logs-for-api-gateway/select-cloudwatch-service.png)

Select **Logs** from the left panel.

![Select CloudWatch logs](/assets/blog/how-to-enable-execution-logs-for-api-gateway/select-cloudwatch-logs.png)

Select the log group that starts with `API-Gateway-Execution-Logs_` followed by the API Gateway id.

![Select log group with API Gateway id](/assets/blog/how-to-enable-execution-logs-for-api-gateway/select-log-group-with-api-gateway-id.png)

You should see 300 log streams ordered by the last event time. This is the last time a request was recorded. Click on the first stream.

![Select first log stream from group](/assets/blog/how-to-enable-execution-logs-for-api-gateway/select-first-log-stream-from-group.png)

This shows you one log entry for each API request. Expand a row, the log data should reflect the format you had previously defined.

![Select log row from API Gateway request](/assets/blog/how-to-enable-execution-logs-for-api-gateway/select-log-row-from-api-gateway-request.png)

Note that, two consecutive groups of logs are not necessarily two consecutive requests in real time. This is because there might be other requests that are processed in between these two that were picked up by one of the other log streams.

#### Summary

This post should give you a good idea of how to enable execution logs for your API Gateway project and also how to view them from the CloudWatch console.
