---
layout: post
title: Deleting Resources
author: aash
---

Seed now gives you the flexibility to delete resources (apps, stages, and services), just from the Seed console.

![App name to confirm deleting app](/assets/blog/deleting-resources/app-name-to-confirm-deleting-app.png)

There might be cases where you just want to remove a stage or service from the Seed console without removing the underlying services. By defaulting to this we make it safer to remove resources from Seed. You can also explicitly choose to remove these resources. Seed will run the [`serverless remove` command](https://serverless.com/framework/docs/providers/aws/cli-reference/remove/) across the app, services, or stages automatically. So you won't have to go through the various deployments to remove them individually. 

You can [read more about deleting resources in our docs]({% link _docs/deleting-resources.md %}).


