---
layout: docs
title: IAM Credentials per Stage
---

While adding your project to [Seed](/), you are required to add the IAM credentials that you are going to deploy with. Seed uses these credentials for deployments to all the different stages. But it is good practice to deploy your stages to separate AWS accounts (or organizations). For example; you can separate your production and dev environments by deploying to completely different AWS accounts.

To configure custom IAM credentials per stage, head over to your app settings and select the stage.

![Select stage](/assets/docs/custom-iam-credentials-per-stage/select-stage.png)

By default, a stage uses the IAM credentials configured for the project.

> A stage defaults to using the project's IAM credentials.

To configure the stage with its own set of IAM credentials, hit **Use Custom IAM**.

![Custom IAM per stage panel](/assets/docs/custom-iam-credentials-per-stage/custom-iam-per-stage-panel.png)

Once this is set, you can trigger a deployment to this stage using the new credentials. Also, this setting applies to all the services in the app.

![Set Custom IAM for stage](/assets/docs/custom-iam-credentials-per-stage/set-custom-iam-for-stage.png)

Just keep in mind that if you are switching AWS accounts for the stage, it'll be better to first remove the existing stage. This will ensure that the resources associated with this stage are removed from the old account.

Finally, you can switch back to using the default project credentials by hitting the **Use Default IAM**.

![Use default IAM for stage](/assets/docs/custom-iam-credentials-per-stage/use-default-iam-for-stage.png)

A quick note on setting the project and stage IAM credentials. A common scheme is to use two AWS accounts for deployment; one for prod and one for all the other stages. In this scenario, it is better to configure the project IAM credentials to the one you'll be using for your non-prod environments. This would ensure that you don't deploy to your prod environment by mistake when adding a new stage.
