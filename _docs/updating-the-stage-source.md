---
layout: docs
title: Updating the Stage Source
---

Once you have your stages/environments configured, you might find yourself needing to change the branch that is tied to it.

This can happen when you are trying to test an update on staging that might not be on `master` (assuming you have staging connected to `master`).

### Update the Source Branch

To change the branch that is tied to a stage, select the stage.

![Select stage](/assets/docs/updating-the-stage-source/select-stage.png)

Click **Settings** and select **Update Source**.

![Click Update Stage Source](/assets/docs/updating-the-stage-source/click-update-source.png)

And select the branch that you'd like to auto-deploy to this stage.

![Select branch to auto-deploy](/assets/docs/updating-the-stage-source/select-branch-to-autodeploy.png)

This will automatically start creating a build in the stage with the selected branch.


### Auto-Deploy Options

By default, auto-deploying for the `prod` or `production` stage is turned off and is turned on for all other stages. This is a good practice since it is better to review your code and infrastructure changes before deploying to production.

However, you might run in to cases where you'd like to configure the auto-deploy setting. To do so, go to the stage settings and select **Enable Auto-Deploy**.

![Enable auto-deploy for production](/assets/docs/updating-the-stage-source/enable-autodeploy-for-prod.png)

Just as the case above, this allows you to select the branch you'd like to auto-deploy. You can also disable auto-deploying at any time in the future by hitting the **Disable Auto-Deploy** button.

![Disable auto-deploy for production](/assets/docs/updating-the-stage-source/disable-autodeploy-for-prod.png)

### Manual Deploy

Finally, you can trigger one-off deployments to a stage from any branch. This can be useful when you want to test a hotfix branch in your staging environment.

To do so, go to the service you want to deploy and hit **Settings**.

![Hit service stage settings](/assets/docs/updating-the-stage-source/hit-service-stage-settings.png)

Select **Trigger Deploy**.

![Select trigger deploy](/assets/docs/updating-the-stage-source/select-trigger-deploy.png)

You'll be asked to pick a branch to deploy.

![Select manual deploy branch](/assets/docs/updating-the-stage-source/select-manual-deploy-branch.png)

And hitting **Deploy Branch** triggers a one-off deployment to the current stage.

By updating the stage source, the auto-deploy options, and the ability to manually deploy; Seed gives you the flexibility to maintain consistent endpoints for your environments while deploying the branch you need.
