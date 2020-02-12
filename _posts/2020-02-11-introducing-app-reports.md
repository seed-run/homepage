---
layout: post
title: Introducing App Reports
image: assets/social-cards/app-reports.png
categories: news
author: frank
---

Introducing App Reports in Seed — a simple way to monitor the performance of your Serverless apps.

<p style="margin: 0 auto; text-align: center;">
  <img src="/assets/blog/introducing-app-reports/introducing-app-reports.png" alt="Serverless App Reports" width="600" />
</p>

App Reports are weekly (or daily) email reports that contain the key metrics for your Serverless apps. They allow you to keep an eye on the performance of your app. It makes it apparent if some of your APIs or Lambda functions have an increase in errors or if they are now performing slower than normal.

Clicking through on the report will take you over to our [metrics viewer]({% link _docs/viewing-metrics.md %}).

![Viewing metrics from App Reports](/assets/blog/introducing-app-reports/viewing-metrics-from-app-reports.png)

Here you can drill down further to [view the logs]({% link _docs/viewing-logs.md %}) for these requests.

![Viewing logs from metrics](/assets/blog/introducing-app-reports/viewing-logs-from-metrics.png)

You can also view the full reports over on the Seed console.

![Complete App Reports in the Seed console](/assets/blog/introducing-app-reports/complete-app-reports-in-the-seed-console.png)

Where you can hide specific Lambda functions from appearing in the reports.

![Hide Lambda functions in App Reports](/assets/blog/introducing-app-reports/hide-lambda-functions-in-app-reports.png)

## Notes

A couple of quick notes on App Reports.

1. It's available to all Seed users.

2. You can switch between receiving them daily or weekly from your organization's settings.

2. App Reports are based on CloudWatch Metrics.

3. AWS will charge you a very small amount for compiling these reports (roughly $0.005 per report depending on the region).

## Summary

App Reports together with the new [metrics]({% link _docs/viewing-metrics.md %}) and [log]({% link _docs/viewing-logs.md %}) viewers allow you to monitor the performance of your Serverless app and quickly diagnose and debug any issues that you might run into. For further details make sure to check out our docs on [viewing App Reports]({% link _docs/viewing-app-reports.md %}).
