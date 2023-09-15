---
layout: post
title: IAM role support
categories: news
image: assets/social-cards/iam-role-support.png
author: frank
---

Seed now connects to your AWS account through IAM roles. It's far more secure than deploying through IAM users.

![Create Seed app IAM role](/assets/blog/iam-role-support/create-seed-app-iam-role.png)

Seed can use an IAM role to generate temporary credentials while deploying. These credentials expire and there's less of a security risk with them getting leaked. So we are **recommending that you update** the credentials in your Seed settings to use IAM roles instead.

If you go in your app settings, you'll notice that we ask you to update to IAM roles. While your current IAM user credentials will continue to work, you should consider making the upgrade as soon as possible.

![Seed app IAM role update message](/assets/blog/iam-role-support/seed-app-iam-role-update-message.png)

Seed will help create a role by deploying a CloudFormation stack into your account. Similar to the IAM user, you can customize the permissions at this step.

![Create IAM role in Seed](/assets/blog/iam-role-support/create-iam-role-in-seed.png)

Once created, copy the **RoleArn** from the outputs in the AWS Console.

![AWS Console IAM role ARN](/assets/blog/iam-role-support/aws-console-iam-role-arn.png)

And paste it in Seed! You can [read more about setting up IAM roles over on our docs]({% link _docs/adding-your-iam-credentials.md %}).
