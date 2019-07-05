---
layout: post
title: Stage Notifications
categories: news
author: jack
---

We rolled out a change to the way you configure build notifications. You can now configure them across all the services in a stage.

You might have noticed that we now allow you to [configure environment variables across all the services in a stage]({% link _posts/2018-11-28-stage-environment-variables.md %}). It is a part of a theme of giving you better control over all your services. Previously, you had to configure both the notifications and environment variables for every single service in a stage. This can be quite tedious when you have a lot of services in your app.

We are simplifying this by allowing you to go to a stage and setting up the notifications for all the services in that stage as a whole.

You can read more about [adding build notifications in our docs]({% link _docs/adding-build-notifications.md %}). This is just one way Seed makes it easier for you to manage your [Serverless Framework](https://serverless.com) applications on [AWS](https://aws.amazon.com).
