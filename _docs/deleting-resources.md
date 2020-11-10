---
layout: docs
title: Deleting Resources
---

Seed gives you the option to delete an app, a stage, or a service and also to remove the deployed resources using a `serverless remove` command.

Let's take a look at how to delete an app.

### Removing an App

Head over to the **Delete** panel in the **Settings** of an app.

![Delete panel in app settings](/assets/docs/deleting-resources/delete-panel-in-app-settings.png)

Here you are asked to enter the app name to confirm deleting the app.

![App name to confirm deleting app](/assets/docs/deleting-resources/app-name-to-confirm-deleting-app.png)

Note that, by default this removes the app **from Seed** and **from AWS**. To remove the app only from Seed, you'd need to deselect the checkbox.

Selecting this checkbox does the following for the respective cases via a set of `serverless remove` commands:

- App: Delete all the deployed services in all the stages.
- Stage: Delete all the deployed services in the stage.
- Service: Delete the deployed service in the various stages.

### Removing a Stage

Similar to the app, you can head over to a stage's **Settings**.

![Removing a stage](/assets/docs/deleting-resources/removing-a-stage.png)

### Removing a Service

For a service, head over to the service's **Settings**.

![Removing a service](/assets/docs/deleting-resources/removing-a-serivce.png)

So if you are looking to delete an app, stage, or service; you need to figure out if you are trying to just remove it from Seed or if you are trying to remove the deployed AWS resources.

Removing the deployed resources from AWS can sometimes take quite long and you might run into some errors. Seed automatically retries the process for certain errors. You can read more about this over on our doc on [Auto-Retrying Serverless Errors]({% link _docs/auto-retrying-serverless-errors.md %}#auto-retrying-on-remove).

### Removing a monorepo app

If your app has multiple services that [are deployed in phases]({% link _docs/configuring-deploy-phases.md %}), Seed will **remove them in the reverse order**.

To understand how this works, it helps to look at an example. Let's assume your services; `serviceA`, `serviceB`, and `serviceC` are deployed in the following order: `serviceA` > `serviceB` > `serviceC`. When a stage is removed, they'll be removed in reverse; `serviceC` > `serviceB` > `serviceA`. This is to handle the case where a service might be referencing a resource from one that was deployed before it. 
