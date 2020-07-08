---
layout: docs
title: Adding a Service
---

Seed supports [monorepo Serverless applications]({% link _docs/mono-repo-apps-in-seed.md %}). This means that you can have multiple Serverless Framework projects (services) in the same repo.

Once your app is created, you can add other services to it by hitting the **New Service** from your app pipeline.

![Click Add a service](/assets/docs/adding-a-service/click-add-a-service.png)

Here you can point to the `serverless.yml` of the service you want to add.

![Set service serverless.yml path](/assets/docs/adding-a-service/set-service-serverless-yml-path.png)

Once Seed finds the file you can add the service. It will also auto-detect the name of the service from the `serverless.yml` file. You can change this later from the service settings.

![Detected service serverless.yml](/assets/docs/adding-a-service/detected-service-serverless-yml.png)

If you don't have a `serverless.yml` for the service yet, you can still add the service anyway. You'll need to specify the **name of the service** manually. And make sure to add the file or change the path to it later.

![Service serverless.yml not found](/assets/docs/adding-a-service/service-serverless-yml-path-not-found.png)

Once you add the service, you'll notice that it's deployed across all the stages that you have configured for your app. This means that a commit to `master` (for example), would trigger a build in the **dev** stage for all the services in the app.

![Service across all stages](/assets/docs/adding-a-service/service-across-all-stages.png)

You can also trigger a build for a specific service in a stage by [manually triggering a deploy for it]({% link _docs/updating-the-stage-source.md %}#manual-deploy).

### Newly created services

While working on a new service, you might want to add it to Seed in a specific stage first. For example, your dev stage might be tied to `master`, while you might have a feature branch called `new-service` that's being deployed to a separate stage. Assume that the `new-service` branch has the new service that you've just added to the pipeline. This service cannot be deployed in dev because the service does not exist in the `master` branch.

For these cases, Seed uses the following scheme:

- If deploying a stage that doesn't have the new service (dev in our example), the service is not deployed and it's marked as **Skipped**.
- The skipped service does not affect the overall status of the build. 
- However, if all services in a build are **Skipped**, the build is marked as **Failed**. This is because nothing was deployed in that build.

![Skipped service build log](/assets/docs/adding-a-service/skipped-service-build-log.png)

For further details on what can cause builds to be skipped, refer to our [chapter on skipped builds]({% link _docs/skipped-builds.md %}).
