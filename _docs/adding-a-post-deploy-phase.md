---
layout: docs
title: Adding a Post-Deploy Phase
---

With mono-repo deployments, you often want to run your integration tests after all your services have been deployed. To do this, Seed allows you to configure a post-deploy phase. A post-deploy phase can include a set of commands that you want to run after all your services have been successfully deployed.

> Seed can run your integration tests as a part of the post-deploy phase.

A post-deploy phase can also be used to run any database migration scripts or any other post-deployment scripts. Post-deploy phases are configured on a per stage basis. This means that you can customize what you want to run, in say production vs your dev stage.

> Post-deploy phases are configured on a per stage basis.

To configure a post-deploy phase, head over to the settings for the stage you are looking to set it for. And hit **Enable Post-Deploy**.

![Enable Post-Deploy Phase](/assets/docs/adding-a-post-deploy-phase/enable-post-deploy-phase.png)

Here you can set the commands you'd like to run. Each line contains its own command. Finally, hit **Save** once you are done.

![Edit Post-Deploy Phase](/assets/docs/adding-a-post-deploy-phase/edit-post-deploy-phase.png)

Now any deployments to this stage will run your commands as a part of the post-deploy phase in the deployment workflow.

![Post-Deploy Phase in Deployment workflow](/assets/docs/adding-a-post-deploy-phase/post-deploy-phase-in-deployment-workflow.png)

And that's it, now you can add your integration tests and post-deployment scripts to your mono-repo workflow.
