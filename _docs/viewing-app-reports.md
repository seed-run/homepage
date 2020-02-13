---
layout: docs
title: Viewing App Reports
---

[Seed](/) periodically compiles a report for your app using CloudWatch to give you an overview of your Lambda and API metrics. This includes the number of requests, number of errors, and latency of your Lambda function or API endpoint.

App Reports are generated for all the apps in your organization.

<p style="margin: 0 auto; text-align: center;">
  <img src="/assets/docs/viewing-app-reports/app-report-email.png" alt="App Report email" width="600" />
</p>

App Reports allow you to keep an eye on the performance of your app. It makes it apparent if some of your APIs or Lambda functions have an increase in errors or if they are now performing slower than before.

By default, these reports are sent out once a week (on Monday around 2am UTC) but they can be configured to be sent daily (around 1am UTC). You can find these in your organization's settings.

![App report in org settings](/assets/docs/viewing-app-reports/app-report-in-org-settings.png)

Note that, since these reports rely on CloudWatch, AWS will charge you a small amount based on your region. It's roughly $0.005 per report. Make sure to check the [CloudWatch Metrics pricing](https://aws.amazon.com/cloudwatch/pricing/) for your region.

### Hiding Lambdas in Reports

Viewing the full report on the Seed console allows you to hide specific Lambdas. For example, you might not be interested in the duration information for a specific Lambda.

![Hide Lambda in reports](/assets/docs/viewing-app-reports/hide-lambda-in-reports.png)

The hidden Lambdas will not be shown in the email but are still available in the console.

### Additional IAM Permissions

To connect to CloudWatch in your AWS account and generate these reports, Seed needs the following set of additional permissions.
  
``` json
{
  "PolicyName": "Reports",
  "PolicyDocument": {
    "Version": "2012-10-17",
    "Statement": [
      {
        "Effect": "Allow",
        "Action": [
          "apigateway:GET",
          "cloudwatch:GetMetricData",
          "cloudformation:ListStackResources"
        ],
        "Resource": "*"
      }
    ]
  }
}
```

App Reports are a great compliment to the [metrics]({% link _docs/viewing-metrics.md %}) and [log]({% link _docs/viewing-logs.md %}) viewer in Seed. Together they allow you to monitor and debug any issues in your app.
