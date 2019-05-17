---
layout: docs
title: Adding a Service
---

Seed supports [mono-repo Serverless applications]({% link _docs/mono-repo-apps-in-seed.md %}). This means that you can have multiple Serverless Framework projects (services) in the same repo.

Once your app is created, you can add other services to it by hitting the **Add a Service** from your app pipeline.

![Click Add a service](/assets/docs/adding-a-service/click-add-a-service.png)

Here you can point to the `serverless.yml` of the service you want to add.

![Set service serverless.yml path](/assets/docs/adding-a-service/set-service-serverless-yml-path.png)

Once Seed finds the file you can add the service. It will also auto-detect the name of the service from the `serverless.yml` file. You can change this later from the service settings.

![Detected service serverless.yml](/assets/docs/adding-a-service/detected-service-serverless-yml.png)

If you don't have a `serverless.yml` for the service yet, you can still add the service anyway. Just make sure to add the file or change the path to it later.

![Service serverless.yml not found](/assets/docs/adding-a-service/service-serverless-yml-path-not-found.png)

Once you add the service, you'll notice that it's deployed across all the stages that you have configured for your app. This means that a commit to `master` (for example), would trigger a build in the **dev** stage for all the services in the app.

![Service across all stages](/assets/docs/adding-a-service/service-across-all-stages.png)

You can also trigger a build for a specific service in a stage by [manually triggering a deploy for it]({% link _docs/updating-the-stage-source.md %}#manual-deploy).
