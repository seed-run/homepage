---
layout: post
title: Why deploy your Serverless app into multiple AWS accounts?
image: assets/social-cards/multiple-accounts.png
description: In this post we'll be looking at why deploying your Serverless app to multiple AWS accounts is a good practice. We'll look at the idea of protecting your production environments, separating resource limits, and consolidated billing across accounts.
categories: tips
author: jack
---


The general idea is to deploy each of your environments to a separate AWS account. Or at the very least keep your _production_ environment separate from the rest of your environments (_dev_, _staging_, _QA_, etc.).

At first glance, this might just seem like a whole lot of extra work and you might wonder if the added complexity is worth while. However, this really helps protect your _production_ environment. And we'll go over the various ways it does so. 

### Environment Separation

Imagine that you (or somebody on your team) removes a DynamoDB table or Lambda function in your `serverless.yml` definition. And instead of deploying it to your _dev_ environment, you accidentally deploy it to _production_. This happens more often than you think!

To avoid mishaps like these, not every developer on your team should have access or direct access from their terminal to the _production_ environment. However, if all your environments are in the same AWS account, you need to carefully craft a detailed IAM policy to restrict/grant access to specific resources for a given environment. This can be hard to do and you are likely to make mistakes.

By keeping each environment in a separate account, you can manage user access on a per account basis. And for _dev_ environments you could potentially grant your developers _AdministratorAccess_ without worrying about the specific resources.

### Resource Limits

Another benefit of separating environments across AWS accounts is helping you work with AWS' service limits. You might be familiar with the various hard and soft limits of the AWS services you use. Like the [Lambda's 75 GB code storage limit](https://docs.aws.amazon.com/lambda/latest/dg/limits.html) or [the total number of S3 buckets per account](https://docs.aws.amazon.com/AmazonS3/latest/dev/BucketRestrictions.html). These limits are applicable on a per account basis. Therefore, an issue with having a single AWS account for all your environments is that, hitting these limits can affect your production environment.

For example, you are likely going to deploy to your _dev_ environment an order of magnitude more than to your _production_ environment. Meaning that you'll hit the Lambda code storage limit on your _dev_ environment quicker than on _production_. And if you only have one account for all your environments, hitting this limit would critically affect your production builds to fail.

By using multiple AWS accounts, you can be sure that the service limits will not interfere across environments.


### Consolidated Billing

Finally, having separate accounts for your environments is recommended by AWS. And AWS has great support for it as well. In the AWS Organizations console, you can view and manage all the AWS accounts in your root account.

![AWS Organizations Console screenshot](/assets/blog/why-deploy-your-serverless-app-into-multiple-aws-accounts/aws-organizations-console-screenshot.png)

You don't have to setup the billing details for each account. Billing is consolidated to the main account. You can also see a breakdown of usage and cost for each service in each account.

#### Summary

This post should give you a good idea why it's recommended to deploy your environments to separate AWS accounts for your Serverless app. If you are currently deploying all your environments to a single AWS account, a good way to split it up would be to slowly move your non-production environments to a new AWS account. We are going to cover this is a lot more detail in an upcoming post.

If you are looking for a way to configure your CI/CD pipelines to deploy to multiple accounts, our posts on [CircleCI]({% link _posts/2019-07-09-how-to-build-a-cicd-pipeline-for-serverless-apps-with-circleci.md %}) and [Travis CI]({% link _posts/2019-07-16-how-to-build-a-cicd-pipeline-for-serverless-apps-with-travis-ci.md %}) cover this in detail. And for [Seed](/), we have [built-in support for multiple AWS accounts]({% link _docs/iam-credentials-per-stage.md %}). So it's even easier to implement this best-practice!
