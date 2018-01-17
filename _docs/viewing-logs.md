---
layout: docs
title: Viewing Logs
---

Seed makes it very easy to monitor your deployments by giving you a live look at your API Gateway Access Logs and Lambda Logs. This allows you to monitor your deployments and decide if you need to rollback in case of an error.

### Lambda Logs

To view the Lambda logs for a stage, simply head over to the stage and click on **View Deployment**.

![View Deployment](/assets/docs/viewing-logs/view-deployment.png)

Here Seed gives you a clear overview of the Lambda functions that have been deployed. And we also show you the API Gateway endpoint for this stage.

![Deployment Info](/assets/docs/viewing-logs/deployment-info.png)

And hit **View Logs**.

![Lambda Logs](/assets/docs/viewing-logs/lambda-logs.png)

This pulls up the logs for a set amount of time. In this case it displays the logs for the last 15mins. Alternatively, you can switch to the **Live** view to monitor the logs as they come in.

![Lambda Logs Live](/assets/docs/viewing-logs/lambda-logs-live.png)

### Access Logs

If you have an API Gateway endpoint in your deployment, you can view the access logs for this as well.

API Gateway Access Logs are disabled by default and need to be enabled on AWS. You'd need to create an IAM Role, configure CloudWatch, etc. to do so. We simplify this on Seed.

You can enable it by heading over to the Stage settings and hitting **Enable Access Logs**.

![Enable Access Logs](/assets/docs/viewing-logs/enable-access-logs.png)

With the access logs enabled, you can **View Deployment** and hit **View Access Logs**.

![View Access Logs](/assets/docs/viewing-logs/view-access-logs.png)

Access logs are displayed similar to the Lambda logs. 

![Access Logs](/assets/docs/viewing-logs/access-logs.png)

And you can switch over to the **Live** view to see the logs as they come in.
