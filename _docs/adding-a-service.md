---
layout: docs
title: Adding a Service
---

Seed supports [mono-repo Serverless applications]({% link _docs/mono-repo-apps-in-seed.md %}). This means that you can have multiple Serverless Framework projects (services) in the same repo.

### Default Service

When you first add your Serverless app to Seed, you are given the option of specifying the location of your default service. By default, Seed looks for a `serverless.yml` in your project root. You can change this by specifying a different name and location for this.

For example, you might want to point to a service called `users` in the `/services/users/` directory of your repo.

![Edit default service](/assets/docs/adding-a-service/edit-default-service.png)

### Add a Service 

Once your app is created, you can add other services to it by hitting the **Add a Service** button in the app's **Settings**.

![Click Add a service](/assets/docs/adding-a-service/click-add-a-service.png)

Here you can set the **Name** and **Path** for the service. 

![Set service name and path](/assets/docs/adding-a-service/set-service-name-and-path.png)

A service is deployed across all the stages that you have configured for your app. This means that a commit to `master` (for example), would trigger a build in the **dev** stage for all the services in the app.

![Service across all stages](/assets/docs/adding-a-service/service-across-all-stages.png)

You can also trigger a build for a specific service in a stage by [manually triggering a deploy for it]({% link _docs/updating-the-stage-source.md %}#manual-deploy).
