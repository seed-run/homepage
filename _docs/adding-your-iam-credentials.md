---
layout: docs
title: Adding your IAM Credentials
---

[Seed](/) needs your AWS IAM credentials to deploy your project on your behalf to your AWS account.

The IAM permissions that Seed requires is made up of:

1. The permissions that Seed needs
2. And the permissions Serverless Framework needs to deploy your app

Start by reviewing the permissions that Seed needs.

![Review Seed IAM permissions screenshot](/assets/docs/iam/review-seed-iam-permissions.png)

Next, customize the permissions that Serverless Framework needs to deploy your app. By default these permissions are very broad since this depends specifically on your app. If you are already using a set of IAM permissions to deploy, you can paste them here.

![Customize Serverless Framework IAM permissions screenshot](/assets/docs/iam/customize-serverless-framework-iam-permissions.png)

Alternatively, you can read the [Customizing your IAM Policy]({% link _docs/customizing-your-iam-policy.md %}) chapter; to get a better idea on how to craft an airtight policy.

Once you are done customizing the permissions, Seed will put the two above sets of permissions together. And will help you create an IAM user using CloudFormation.

Hit the **Create with CloudFormation** button.

![Click Create with CloudFormation screenshot](/assets/docs/iam/click-create-with-cloudformation.png)

This will redirect you to CloudFormation on your AWS Console.

![CloudFormation Seed template screenshot](/assets/docs/iam/cloudformation-seed-template.png)

Scroll down to the bottom of the page, hit the **I acknowledge that AWS CloudFormation might create IAM resources.** and click **Create**.

![Click create CloudFormation Seed template screenshot](/assets/docs/iam/click-create-cloudformation-seed-template.png)

CloudFormation will now create a Seed IAM user. This will take a minute or two.

![CloudFormation Seed user creating screenshot](/assets/docs/iam/cloudformation-seed-use-creating.png)

Once complete, expand the **Outputs** section. And copy the **AccessKey** and **SecretKey**.

![CloudFormation complete output screenshot](/assets/docs/iam/cloudformation-complete-output.png)

Paste it back over on Seed.

![Paste IAM credentials on Seed screenshot](/assets/docs/iam/paste-iam-credentials-on-seed.png)

Hit **Add App** to complete creating your app!
