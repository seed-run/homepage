---
layout: docs
title: Viewing Logs
---

Seed makes it very easy to monitor your deployments by giving you a live look at your API Gateway Access Logs and Lambda Logs. This allows you to monitor your deployments and decide if you need to rollback in case of an error.

### Lambda Logs

To view the Lambda metrics for a stage, simply select the stage.

![Select stage](/assets/docs/viewing-logs/select-stage.png)

Click **View Resources** for the service you are looking for.

![Stage view resources](/assets/docs/viewing-logs/stage-view-resources.png)

Here Seed gives you a clear overview of the resources that have been deployed.

![Resources Info](/assets/docs/viewing-logs/resources-info.png)

Hit **Logs** for a Lambda you are interested in.

![Lambda Logs](/assets/docs/viewing-logs/lambda-logs.png)

This pulls up the logs for a set amount of time. In this case it displays the logs for the last 15mins. Alternatively, you can switch to the **Live** view to monitor the logs as they come in.

![Lambda Logs Live](/assets/docs/viewing-logs/lambda-logs-live.png)

Seed also detects any errors in your Lambdas and formats them appropriately.

![Lambda Logs Error](/assets/docs/viewing-logs/lambda-logs-error.png)

### Access Logs

If you have an API Gateway endpoint in your deployment, you can view the access logs for this as well.

API Gateway Access Logs are disabled by default and need to be enabled on AWS. You'd need to create an IAM Role, configure CloudWatch, etc. to do so. We simplify this on Seed.

You can enable it by heading over to the **Deployment Settings** and hitting **Enable Access Logs**.

![Enable Access Logs](/assets/docs/viewing-logs/enable-access-logs.png)

With the access logs enabled, hit **Access Logs** for the API Gateway endpoint.

![Resources info](/assets/docs/viewing-logs/resources-info.png)

Access logs are displayed similar to the Lambda logs. 

![Access Logs](/assets/docs/viewing-logs/access-logs.png)

And you can switch over to the **Live** view to see the logs as they come in.
