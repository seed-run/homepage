---
layout: post
title: Notification for stages that failed to remove
categories: news
author: jack
---

You'll now receive a notification (Slack, email, or Webhook) if there was a problem with removing a stage.

When Seed removes a stage, it removes every single service in that stage. Including all of its resources. And depending on the number of resources and services involved, this process might fail.

![Failed to remove stage in Seed](/assets/blog/notifications-for-stages-that-failed-to-remove/failed-to-remove-stage-in-seed.png)

Usually you'll need to retry removing the stage. But since the process of removing a stage happens in the background; you won't know if there was a problem unless you check the Seed console. This is especially true for stages that are removed automatically. Like when a PR is closed or a branch is removed.

To fix this, Seed will now send you a notification if there was a problem removing a stage. These are sent to the ones configured in [the build notifications]({% link _docs/adding-build-notifications.md %}). And it'll tell you the error and link back to the stage that had the problem.

Failed to remove stage notifications are really helpful if you are using [a PR or branch based workflow]({% link _posts/2019-02-05-git-workflow-updates.md %}) to deploy for your Serverless app.

