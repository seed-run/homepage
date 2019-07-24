---
layout: post
title: How to deploy your Serverless app into multiple AWS accounts?
image: assets/social-cards/multiple-accounts.png
description: In this post we'll look at how to deploy the various environments of your Serverless app to multiple AWS accounts. We'll also look at how to parameterize your resources to avoid any name collisions. And how to conditionally deploy some resources to a stage. Finally, we'll look at a couple of little details to watch out for, while working with multiple AWS accounts.
categories: tips
author: jack
---

Teams commonly use multiple AWS accounts to host the environments (_dev_, _staging_, _prod_, etc.) for their Serverless app. The main reason for this is to protect their production environment. You can read about this in detail in [one of our previous posts]({% link _posts/2019-07-19-why-deploy-your-serverless-app-into-multiple-aws-accounts.md %}).

In this post we are going to look at how to do this for your [Serverless Framework](https://serverless.com) app. Here is the basic idea:

- Serverless Framework has a concept of stages. Make sure to use these stages as an environment.
- You can deploy each stage into a separate AWS account using a different AWS profile. You can do this by using the `--aws-profile` option.
  
  ``` bash
  $ serverless deploy --aws-profile production
  ```

  Where `production` is the name of the AWS profile in your `~/.aws/credentials` file. You can also configure this using the AWS CLI.

  ``` bash
  $ aws configure --profile production
  ```

  We have written about [using multiple AWS profiles in detail over on Serverless Stack](https://serverless-stack.com/chapters/configure-multiple-aws-profiles.html).

- Recall that, Serverless Framework uses CloudFormation behind the scenes to provision AWS resources. The CloudFormation template is generated from your `serverless.yml`. And since the same `serverless.yml` is used to generate the CloudFormation template for all your stages; the resources provisioned for the stages are identical copies of each other.
- This means that your Development, QA, Testing, and Staging environments will be able to mirror the Production environment as closely as possible.

The basic idea here is simple enough; deploy the same stack to multiple accounts using different AWS profiles. Next, let's look at some of the details and a couple of issues that you might run into.

### Parameterize resources names

As we deploy the same stack across all our AWS accounts, we generally don't need to worry about the resource names colliding. However, AWS does have some services (like S3) where the resource names need to be unique across all AWS accounts.

Additionally, if you end up deploying a couple of environments to the same AWS account. Say for example, all your _dev_ environments go to the same AWS account, you might want to parameterize your resource names anyway.

You can do this by including the stage name to be a part of the resource name. So your DynamoDB table name could be:

``` yaml
tableName: ${self:custom.stage}-table
```

Where `self:custom.stage` would be:

``` yaml
stage: ${opt:stage, self:provider.stage}
```

It's highly recommended that you do this for all your resources to exclude the possibility of resource name collisions.

### Customizing stages

You might run into cases where certain resources should not be deployed to all your stages. For example, you might not need a [DAX caching layer](https://aws.amazon.com/dynamodb/dax/) for the DynamoDB tables in your _dev_ stages. However, since we are deploying the exact same stack to all the stages you need to make a small tweak to your `severless.yml`.

The trick is to assign the necessary resources based on the stage. For example, you load your `functions` from:

``` yaml
functions: ${self:custom.functions.${opt:stage}}
```

Where `self:custom.functions` is:

``` yaml
custom:
  functions:
    dev: false
    prod:
      hello:
        handler: handler.main
        events:
          - http:
              path: /
              method: get
```

We have a simple repo showing you [how to optionally deploy resources based on a stage here](https://github.com/seed-run/serverless-example-monorepo-with-conditional-resources).

### Watch out for account limits

A downside of using multiple AWS accounts is that newly created AWS accounts have a lower usage limit on most services. For example, [AWS CodeBuild](https://aws.amazon.com/codebuild/) has a default limit of 20 concurrent running builds. However, new accounts are limited to just 1 concurrent build.

So you'll need to ensure the new account's service limit meets your requirements. And contact AWS support to raise the limits if they don't. You'll need to do this once per AWS account but it can cause problems if you are going to use this in production and you forget to upgrade the limits.

### Watch out for unused resources

As you start working with multiple AWS accounts, you might run into cases where some resources might not get properly removed in an account. This will lead to you having quite a few orphaned resources spread across multiple accounts. This can be a bit of a pain if you've to keep track of them.

A really good way to catch these before they affect your overall bill is by taking advantage of the consolidated billing feature that AWS has. It gives you a good overview across all your AWS accounts and a breakdown on a cost per account per service basis. This lets you identify and remove any unused resources.

Also, note that when you remove an account, it'll automatically de-provision all the resources provisioned in the account. This allows you to clean up after you are done using an environment.

#### Summary

In this post we looked at how to deploy the various environments of your Serverless app to multiple AWS accounts. We also looked at how to parameterize your resources to avoid any name collisions. And how to conditionally deploy some resources to a stage. Finally, we looked at a couple of little details to watch out for, while working with multiple AWS accounts.
