---
layout: docs
title: Manually Deploying
---

You can trigger one-off deployments to any stage or service in Seed. This can be useful for example, when you want to test a hotfix branch in your staging environment.

### Manually Deploy a Stage

To manually deploy a stage, head over to the app pipeline. And hit **Deploy** on the stage you want to manually deploy.

![Select stage](/assets/docs/manually-deploying/select-stage.png)

Here you can confirm the branch you want to deploy with. Or if the stage isn't connected to a branch, you'll be asked to select one.

![Hit stage trigger deploy](/assets/docs/manually-deploying/hit-stage-deploy.png)

You can optionally force a deploy, more on this below.

### Manually Deploy a Service

To deploy a specific service, click the dropdown for the service in the stage you want to deploy. Hit **Deploy Service**.

![Select service dropdown](/assets/docs/manually-deploying/select-service-down.png)

Just as above, you'll be asked to confirm the branch or to select one.

![Hit service trigger deploy](/assets/docs/manually-deploying/hit-service-trigger-deploy.png)

### Force Deploys

By default, Seed will only deploy the services and Lambda functions that have been updated. You can [read more about Incremental Deploys here]({% link _docs/what-are-incremental-deploys.md %}). To skip this check and deploy all your services and Lambdas, select the **Force deploy** option.

![Select force option](/assets/docs/manually-deploying/select-force-option.png)

This option tells Seed to deploy all your services even if there are no changes that've been detected.

A **Force deploy** also clears the [dependency cache]({% link _docs/caching-dependencies.md %}) for the stage you are deploying to.

