---
layout: docs
title: Deleting Resources
---

Seed gives you the option to delete an app, a stage, or a service and also to remove the deployed resources using a `serverless remove` command. Let's take a look at how to delete an app.

Head over to the **Delete** panel in the **Settings** of an app.

![Delete panel in app settings](/assets/docs/deleting-resources/delete-panel-in-app-settings.png)

Here you are asked to enter the app name to confirm deleting the app.

![App name to confirm deleting app](/assets/docs/deleting-resources/app-name-to-confirm-deleting-app.png)

Note that, by default this only **removes the app from Seed**.

To remove the resources that were deployed as a part of this app (in all of its stages and services), you'd need to select the checkbox.

![Select delete resources checkbox](/assets/docs/deleting-resources/select-delete-resources-checkbox.png)

Selecting this checkbox does the following for the respective cases via a set of `serverless remove` commands:

- App: Delete all the deployed services in all the stages.
- Stage: Delete all the deployed services in the stage.
- Service: Delete the deployed service in the various stages.

So if you are looking to delete an app, stage, or service; you need to figure out if you are trying to just remove it from Seed or if you are trying to remove the deployed AWS resources. And remember that by default it only removes it from Seed.
