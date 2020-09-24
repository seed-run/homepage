---
layout: post
title: Fixing CDK Deployments
categories: news
author: frank
tweet: 
---

The [new integrated CDK deployments in Seed]({% link _posts/2020-08-31-sst-deployments-beta.md %}) is the fastest and cheapest way to deploy CDK apps. In this post we'll look at the technical details of how we make it happen.

You might recall that you can now deploy your Serverless infrastructure using [AWS CDK](https://aws.amazon.com/cdk/) on Seed by using the [**Serverless Stack Toolkit**](https://github.com/serverless-stack/serverless-stack) (SST). SST allows you to deploy your CDK apps alongside your Serverless Framework services.

But aside from making CDK compatible with Serverless Framework, SST (along with Seed) does two key things:

1. **Speed up your deployments** by deploying your stacks concurrently
2. **Saves build minutes** by not waiting for CloudFormation to update

Let's look at them in a little more detail.

### 1. Concurrent Deployments

The first big advantage of using CDK with SST is that SST deploys all your CDK stacks concurrently. This is especially beneficial for large apps where each stack can take fairly long to deploy.

SST does this while still respecting the dependencies between your CDK stacks. Meaning, if some of your stacks depend on the output of another, SST will deploy them in order.

### 2. Integrated Deployment Infrastructure

SST is natively integrated with the deployment infrastructure in Seed. And this allows us to make your deployments as efficient as possible.

To understand this, here's what the deployment lifecycle of a CDK app looks like:

1. Install dependencies using npm
2. Convert your CDK app to CloudFormation stacks
3. Submit the stacks and artifacts to CloudFormation
4. Wait for CloudFormation to update your stacks

![CDK deployment lifecycle](/assets/blog/fixing-cdk-deployments/cdk-deployment-lifecycle.png)

The `cdk deploy` command encapsulates step 3 and 4.

Standard CI services (like CircleCI or Travis CI) simply run the build commands you give them. They know very little about the application they are building. A dirty secret about deploying _Infrastructure as code_ (IaC) apps, like CDK or Serverless Framework through a CI service is that, you mostly pay for waiting, not building.

> A dirty secret about deploying Infrastructure as code apps through a CI service is that you mostly pay for waiting, not building.

So a standard CI service will simply run the `cdk deploy` command and wait for CloudFormation to update. This step can take quite long for large stacks. And they'll simply charge you build minutes as you wait.

However, the new integrated deployment infrastructure on Seed plugs right into the CDK deployment lifecycle with SST. This allows us to deploy it as efficiently as possible.

![CDK deployment lifecycle](/assets/blog/fixing-cdk-deployments/cdk-deploy-process-in-seed-with-sst.png)

Seed knows that once the main part of the `cdk deploy` command is done, it can switch over to a separate asynchronous process to monitor the CloudFormation update status. This process is not run on your build machine, and doesn't cost you any build minutes. Making it basically free!

> Seed uses a separate asynchronous process to check your CloudFormation status that doesn't cost you any build minutes.

And of course, Seed can do this in parallel for all your stacks.

### 3. Caching & Other Optimizations

The integrated deployment infrastructure that we created is specific for CDK apps deployed using SST. So it allows us to cache the necessary dependencies. We also have a ton of other optimizations under the hood that allows us to ensure that subsequent deployments are as fast as possible. All without you having to configure anything.

## Closing

Thanks to concurrent deployments and the integrated deployment infrastructure for CDK apps; Seed is now the fastest and most efficient way to deploy CDK. It deploys all your stacks concurrently and doesn't waste any build minutes waiting for CloudFormation to update.

So you get **5x faster** deploys that are practically **free**!

![CDK deployments CircleCI vs Seed](/assets/blog/fixing-cdk-deployments/cdk-deployments-circleci-vs-seed.png)

For comparison, a standard CDK app with 7 stacks (a few DynamoDB tables, SNS topics, and SQS queues), deployed on CircleCI takes 417 seconds. While that same app deployed on Seed using SST takes 100 seconds. And subsequent deployments take 193 seconds on CircleCI vs. 40 seconds on Seed.

So [checkout our docs on adding SST apps to Seed]({% link _docs/adding-a-cdk-app.md %}) and give it a try!
