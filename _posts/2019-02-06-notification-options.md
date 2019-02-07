---
layout: post
title: Notification Options
author: jack
---

We made a small update to the build notifications in Seed. You can now choose to be notified for build failures only.

![Build notification options](/assets/blog/notification-options/build-notification-options.png)

Seed can notify you via email, Slack, or a custom webhook on the status of your builds. If you are continuously committing changes, you might be getting too many notifications. And if most of your builds are successful these notifications can get annoying. To fix this, you can now choose to be notified only when a build fails. You can select the notification event while adding a new notification option. Read more about this in the [build notifications chapter]({% link _docs/adding-build-notifications.md %}) in our docs.

By giving you better control over your build notifications, Seed makes it simple to manage your CI/CD pipeline for Serverless Framework applications on AWS.

