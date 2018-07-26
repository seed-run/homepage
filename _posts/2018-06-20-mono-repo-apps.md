---
layout: post
title: Mono-Repo Apps
image: /assets/social-cards/mono-repo-apps.png
author: frank
---

Mono-repo support in Seed is now publicly available. With this change, a Serverless app can have multiple services within it. Seed will also deploy all the services within your app concurrently.

You can read more about [services in Serverless Framework here](https://serverless.com/framework/docs/providers/aws/guide/services/). And the [popular patterns for organizing Serverless projects](https://serverless-stack.com/chapters/organizing-serverless-projects.html).

![App Pipeline view](/assets/blog/mono-repo-apps/app-pipeline-view.png)

Seed will also manage the environments across all the services in your app. And changing the settings for a stage will apply those changes to all the services in the stage.

![App Stage settings](/assets/blog/mono-repo-apps/app-stage-settings.png)

While an app in Seed can have multiple services; it defaults to looking for a `serverless.yml` in the root of the project. This means that if you are using a multi-repo setup, with each service in a separate repo; Seed will continue to work just as before without any changes.

You can read more about mono-repo support in our docs:

- [Mono-repo apps in Seed]({% link _docs/mono-repo-apps-in-seed.md %})
- [Adding a service]({% link _docs/adding-a-service.md %})

With mono-repo support, Seed now provides a complete CI/CD pipeline for Serverless applications!
