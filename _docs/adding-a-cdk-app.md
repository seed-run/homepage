---
layout: docs
title: Adding a CDK App
---

Seed supports deploying AWS CDK apps with [SST](https://github.com/sst/sst). SST makes it easy to build serverless apps by using CDK constructs to define your infrastructure. And you can use it alongside your Serverless Framework services.

### Advantages of CDK and SST on Seed

1. The fastest way to deploy CDK apps

   SST supports concurrently deploying all the stacks in your CDK apps. SST is also natively supported in Seed and features a custom deployment infrastructure that's specifically optimized for it. Making Seed the fastest way to deploy your CDK apps

2. Free

   Seed directly plugs into the SST deployment process. So when a CDK app is waiting for CloudFormation to update your stacks, Seed pauses the build process and does this asynchronously. This allows Seed to make CDK deployments very efficient and offer it to you for free!

You can [read more about this in our post here]({% link _posts/2020-09-23-fixing-cdk-deployments.md %}). Note that, there are [a couple of pricing limits that we talk about below](#pricing-limits).

> CDK deployments on Seed are free!

Let's look at how to add a new SST app to Seed.

### Adding a New App

While adding a new app, pick the repo with your SST app in it.

![Select repo with CDK SST app](/assets/docs/adding-a-cdk-app/select-repo-with-cdk-sst-app.png)

And Seed will look for any `sst.config.ts` files in your repo.

![Detected sst.config.ts in repo](/assets/docs/adding-a-cdk-app/detected-sst-config-ts-in-repo.png)

Pick the SST app you want to add. If you've got multiple SST apps or Serverless services, you can add them later.

![Adding CDK SST app](/assets/docs/adding-a-cdk-app/adding-cdk-sst-app.png)

Next, you'll be asked to [add the IAM credentials for your dev and prod environments]({% link _docs/adding-your-iam-credentials.md %}).

### Pricing Limits

CDK apps deployed using SST on Seed are free. There are a couple of small limitations to this:

1. If you are running additional scripts as a part of your [build spec]({% link _docs/adding-a-build-spec.md %}), you'll be billed for the build minutes it takes to run those scripts.
2. Seed installs your npm packages as a part of the build process. If this step takes longer than 180s, you'll be billed for it. For example, if it takes 282s, you'll be billed for 282 - 180 = 102s.
3. Applies to the [Standard build machine]({% link _docs/build-machine-types.md %}).
4. For all other build machines, you're not charged for the time spent waiting for CloudFormation to update. But you are charged for the time it takes to build your app.
