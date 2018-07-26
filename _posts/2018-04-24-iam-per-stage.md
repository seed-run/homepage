---
layout: post
title: IAM Credentials per Stage
author: aash
---

You can now set custom IAM credentials for a stage. Now you can deploy to stages that are in completely separate AWS Organizations!

![Custom IAM per stage panel](/assets/blog/iam-credentials-per-stage/custom-iam-per-stage-panel.png)

It is very common for teams to completely isolate their environments using separate AWS Organizations. So for example, you could have all your development environments in one organization, while your _production_ environment is in a different one.

You can [read more about AWS Organizations here](https://aws.amazon.com/organizations/) and also about how [IAM policies work with Organizations](https://aws.amazon.com/premiumsupport/knowledge-center/iam-policy-service-control-policy/).

By default, Seed will deploy using the IAM credentials that you have configured for the project. And you can override this by setting up a specific set of IAM credentials for a stage.

Support for AWS Organizations and multiple IAM credentials in Seed allows you to easily configure your Serverless CI/CD pipeline across your team.

You can [read more about setting up IAM credentials per stage in our docs]({% link _docs/iam-credentials-per-stage.md %}).
