---
layout: page
title: Promoting to Production
---

Seed creates two default stages when a project is added. A **dev** stage that builds project's default Git repository branch (usually the **master** branch) and a **production** stage that can only be deployed by promoting a working build from a development stage. A Seed project will always have exactly one production stage, and it cannot be removed. However, you can add more development stages that track a specific [branch]({% link _docs/adding-a-stage.md %}) or a [pull request]({% link _docs/working-with-pull-requests.md %}).

> The production stage in Seed does not track a branch and cannot be removed

The main reason for this is because code and infrastructure are closely coupled in Serverless. And every single deploy can include some infrastructure changes. This coupling is incredibly convenient and powerful. Internally, CloudFormation figures out which parts of your infrastructure are being added, modified, or removed.

To ensure that you have a clear idea of the infrastructure changes that are being deployed, Seed generates a changeset for each build. Promoting to production requires you to manually review the stack changes that are going to be applied.

> You need to review the infrastructure changes before promoting to production

We think this extra step can help prevent any irreversible infrastructure changes from being deployed to your production environment mistakingly.

Let's look at this in a bit more detail.

To get started, select the development stage you want to promote. All development stages tracking either a Git branch or a pull request can be promoted.

![Select Stage To Promote](/assets/docs/promoting-to-production/select-stage-to-promote.png)

You can only promote the current working build. Select **Promote**.

![Promote Stage](/assets/docs/promoting-to-production/promote-stage.png)

When a project is deployed, Serverless Framework generates a new CloudFormation template file based on the resources defined in **serverless.yml**, and submits the template to CloudFormation. CloudFormation will then apply the resource changes. A mistake in the resource definition can lead to permanent data loss and/or a security breach, which can be very costly in the **production** environment.

Seed allows you to review the changes that are about to be applied in the **production** stage prior to promoting a development build. This is achieved by generating a CloudFormation changeset with the new stack template.

![Review Changeset](/assets/docs/promoting-to-production/review-changeset.png)

The changeset shows all the AWS resources about to be added, removed, and modified. Be sure to review these carefully. After you review and **confirm** the changeset, the build will be promoted and the **production** stage will be updated.

![Confirm Changeset](/assets/docs/promoting-to-production/confirm-changeset.png)

After the update is complete, the build is marked as **Promoted**.

![Stage Promoted](/assets/docs/promoting-to-production/stage-promoted.png)

If the promoted build is faulty, you can go into the **Production** stage and hit **Rollback** to revert to a previous build.

![Rollback Production](/assets/docs/promoting-to-production/rollback-production.png)

Conceptually, rolling back is like applying a previous update on the current project. This means that any data removed in an update will not be restored upon rollback.
