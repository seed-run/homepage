---
layout: post
title: Improved IAM Permission Requests
categories: news
author: jack
---

Seed will now show you specific details for the IAM permissions it needs for a specific feature. This makes it easier to grant the exact IAM permissions for the necessary resources.

![Detailed IAM permissions requested](/assets/blog/improved-iam-permission-requests/detailed-iam-permissions-requested.png)

Over the past few months Seed has launched a few new features (like [Logs]({% link _posts/2020-01-06-new-and-improved-serverless-logs.md %}), [Metrics]({% link _posts/2020-01-21-new-and-improved-serverless-metrics.md %}), and [App Reports]({% link _posts/2020-02-11-introducing-app-reports.md %})). Some of these require additional IAM permissions. However, adding these additional permissions can be difficult if you are granting fine-grained IAM permissions to Seed. To address this, Seed now shows you exactly which permission is required for the resource in question. This allows you to better craft fine-grained controls. And for reference you can see the entire set of permissions that are necessary for this feature.

By helping you manage granular IAM permissions, Seed makes it easy to build and deploy secure Serverless applications.

