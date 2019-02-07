---
layout: post
title: Better Error Messages
author: jack
---

We pushed an update to display better build error messages. Seed will now extract the error messages generated as a part of the build process to make it easier to debug.

![Seed build error message](/assets/blog/better-error-messages/seed-build-error-message.png)

We look through the build logs to figure out what exactly went wrong. We also pass this error message in our notifications so you can debug the issue right away. We know that when a build fails, the last thing you want to do is wade through pages of build logs to figure out what went wrong.

![Seed build error email notification](/assets/blog/better-error-messages/seed-build-error-email-notification.png)

By accurately displaying build error messages, Seed makes it easy to manage the deployment process for your Serverless Framework apps.
