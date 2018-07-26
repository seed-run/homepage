---
layout: post
title: Custom Webhooks
image: /assets/social-cards/custom-webhooks.png
author: aash
---

Seed now supports custom webhooks as a way to be notified on the progress of a build. Simply, add the webhook URL and optionally specify a JWS secret token.

![Add webhook notification](/assets/blog/custom-webhooks/add-webhook-notification.png)

And Seed will send you a notification with the status set to either `deploying`, `success`, or `failure`.

You can configure webhook notifications for a specific stage. So for example, you can turn on notifications for the _production_ stage only. With the simple yet targeted email, slack, and webhook notifications; Seed helps your team better manage deployments for your Serverless projects.

You can [read more about adding build notifications in our docs]({% link _docs/adding-build-notifications.md %}).
