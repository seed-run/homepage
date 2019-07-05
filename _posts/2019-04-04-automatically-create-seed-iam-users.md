---
layout: post
title: Automatically Create Seed IAM Users
categories: news
author: jack
---

Seed now helps you automatically create an IAM user to manage your deployments.

![Seed create IAM user with CloudFormation](/assets/blog/automatically-create-seed-iam-users/seed-create-iam-user-with-cloudformation.png)

Previously, we left it up to you to create an IAM user to manage your app on Seed. This included the cumbersome process of customizing the premissions needed.

Seed now guides you through this process by using CloudFormation to create the IAM user. You start by reviewing the permissions that Seed needs.

![Review Seed IAM permissions](/assets/blog/automatically-create-seed-iam-users/review-seed-iam-permissions.png)

Next, you can supply the permissions that Serverless Framework needs to deploy your app. 

![Customize Serverless Framework permissions](/assets/blog/automatically-create-seed-iam-users/customize-serverless-framework-permissions.png)

Seed will then combine these two sets of permissions and generate a CloudFormation template that will help you create an IAM user.

![CloudFormation create Seed user](/assets/blog/automatically-create-seed-iam-users/cloudformation-create-seed-user.png)

Once the stack has completed creating, simply copy and paste the AccessKey and SecretKey over to Seed!

You can read more on how to [create a Seed IAM user]({% link _docs/adding-your-iam-credentials.md %}) and how to [customize your IAM policy]({% link _docs/customizing-your-iam-policy.md %}) over on our docs. By simplifying the process of creating an IAM user, Seed is helping you manage deployments for your Serverless Framework projects on AWS.
