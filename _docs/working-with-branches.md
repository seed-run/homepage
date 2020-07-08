---
layout: docs
title: Working with Branches
---

Stages in Seed are usually tied to a Git branch. You can read more about [adding a stage here]({% link _docs/adding-a-stage.md %}). Seed can also automatically create stages when a new Git branch is created.

Head over to your app and select the **Pipeline** tab.

![App Pipeline](/assets/docs/working-with-branches/app-pipeline.png)

Select **Edit Pipeline**.

![Enable auto deploy branches](/assets/docs/working-with-branches/enable-auto-deploy-branches.png)

Here you can specify a stage to copy the environment variables and other settings from. For example, your `dev` stage might be configured with environment variables for your app and with a set of IAM credentials specific for dev deployments. By selecting the `dev` stage, any stage that is automatically created for a new branch will copy the settings from the `dev` stage.

Seed will copy the following settings (if available) from the selected stage:

- IAM settings
- Post-deploy phase
- Notification settings
- Environment variables

![Auto-deploy branch settings](/assets/docs/working-with-branches/enable-auto-deploy-branch-settings.png)

You can also specify what you want to do once the branch is closed. By hitting the **Remove the stage and all the resources when the branch is deleted** checkbox, you are telling Seed to remove the automatically deployed stage and all the resources. You can always manually remove these stages by [following the steps in this chapter]({% link _docs/deleting-resources.md %}#removing-a-stage).

Once you hit **Enable Auto-Deploy**, any new Git branches that are created will create a new stage in Seed automatically!
