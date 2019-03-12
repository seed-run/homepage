---
layout: docs
title: Promoting to Production
---

Seed creates two default stages when a project is added. A **dev** stage that builds project's default Git repository branch (usually the **master** branch) and a **production** or **prod** stage that by default can be deployed by promoting a working build from a development stage. A Seed app will always have exactly one production stage, and it cannot be removed.

The reason we support a manual promotion step is because code and infrastructure are closely coupled in Serverless. A single deploy can include some infrastructure changes. This coupling is incredibly convenient and powerful. Internally, CloudFormation figures out which parts of your infrastructure are being added, modified, or removed.

To ensure that you have a clear idea of the infrastructure changes that are being deployed, Seed generates a [CloudFormation Change Set](https://aws.amazon.com/blogs/aws/new-change-sets-for-aws-cloudformation/) for each build. Promoting to production requires you to manually review the stack changes that are going to be applied. The Change Sets are generated using the build artifacts that were created as a part of the build process. You can read more about them in the [Generating Trusted Builds]({% link _docs/generating-trusted-builds.md %}) chapter.

> You need to review the infrastructure changes before promoting to production

We think this extra step can help prevent any irreversible infrastructure changes from being deployed to your production environment mistakingly. However, we understand that you might run into cases where you'd like to auto-deploy to production. For this you can follow the steps in the [Updating the stage source]({% link _docs/updating-the-stage-source.md %}#auto-deploy-production) chapter to enable it.

Let's look at this in a bit more detail.

### Promoting a Stage

From your app homepage you can get a clear picture of the various stages, service, and builds in them.

To promote a stage to production, hit the **Promote** button for the stage you want to promote.

![Select Stage To Promote](/assets/docs/promoting-to-production/select-stage-to-promote.png)

When a service is deployed, Serverless Framework generates a new CloudFormation template file based on the resources defined in **serverless.yml**, and submits the template to CloudFormation. CloudFormation will then apply the resource changes. A mistake in the resource definition can lead to permanent data loss and/or a security breach, which can be very costly in the **production** environment.

Seed allows you to review the changes that are about to be applied in the **production** stage prior to promoting a development build. This is achieved by generating a CloudFormation Change Set with the new stack template.

The Change Set shows all the AWS resources about to be added, removed, and modified. Be sure to review these carefully. After you review and **confirm** the Change Set, the build will be promoted and the **production** stage will be updated.

When you promote a stage, Seed will give you a chance to review the CloudFormation Change Sets for the services in the stage.

![Confirm Change Set](/assets/docs/promoting-to-production/confirm-change-set.png)

Once confirmed, you'll notice that the services in the production stage are busy applying these changes.

![Production stage in progress](/assets/docs/promoting-to-production/production-stage-in-progress.png)

### Promoting a Service

Seed also gives you the flexibility to promote individual services. To do this, select a service.

![Select service](/assets/docs/promoting-to-production/select-service-to-promote.png)

Just as above, hit **Promote** for the stage you are trying to promote.

![Hit promote service](/assets/docs/promoting-to-production/hit-promote-service.png)

And you'll be asked to confirm the changes here as well.

![Confirm service Change Set](/assets/docs/promoting-to-production/confirm-service-change-set.png)

Once you confirm, the specific service in this stage will be promoted to production.
