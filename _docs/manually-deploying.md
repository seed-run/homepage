---
layout: docs
title: Manually Deploying
---

You can trigger one-off deployments to any stage or service in Seed. This can be useful for example, when you want to test a hotfix branch in your staging environment.

### Manually Deploy a Stage

To manually deploy a stage, head over to the app pipeline.

![Select stage](/assets/docs/manually-deploying/select-stage.png)

And hit **Deploy** on the stage you want to manually deploy.

![Hit stage trigger deploy](/assets/docs/manually-deploying/hit-stage-deploy.png)

Here you'll be prompted to select a branch you want to deploy with. Or if this stage has a branch connected to it, you'll be asked if you want to deploy using it.

![Trigger deploy select branch](/assets/docs/manually-deploying/trigger-deploy-select-branch.png)

You can optionally force a deploy using the [Serverless Framework](https://serverless.com) `--force' flag. By default, Serverless Framework only deploys the services that have been updated. The `--force` option overrides this and deploys even if there are no changes.

![Force deploy option](/assets/docs/manually-deploying/force-deploy-option.png)

### Manually Deploy a Service

To deploy a specific service, click the dropdown for the service in the stage you want to deploy.

![Select service dropdown](/assets/docs/manually-deploying/select-service-down.png)

Hit **Deploy Service**.

![Hit service trigger deploy](/assets/docs/manually-deploying/hit-service-trigger-deploy.png)

Just as above, you'll be asked to select a branch.


### Force Deploys

By default, Serverless Framework only deploys the services that have changed. It does this by comparing the code package and the CloudFormation template. However, there might be cases where you want to override this behavior. You can do this by selecting the **Force deploy** option from the manual deploy dialog.

![Select force option](/assets/docs/manually-deploying/select-force-option.png)

This option tells Seed to deploy using the Serverless Framework `--force` flag and deploy even if there are no changes.
