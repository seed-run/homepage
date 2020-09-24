---
layout: docs
title: Adding a CDK App
---

Seed supports deploying AWS CDK apps with SST. [**SST** or Serverless Stack Toolkit](https://github.com/serverless-stack/serverless-stack) makes it possible to deploy CDK apps alongside your Serverless Framework services. It allows you to deploy your CDK app to multiple stages, region, or AWS accounts. Just like you would for your Serverless services.

### Advantages of using CDK with SST

Aside from allowing you to use CDK alongside your Serverless Framework services, SST has a couple of other key advantages. SST on Seed is:

1. The fastest way to deploy CDK apps

   SST supports concurrently deploying all the stacks in your CDK apps. SST is also natively supported in Seed and features a custom deployment infrastructure that's specifically optimized for it. Making Seed the fastest way to deploy your CDK apps

2. Practically free

   Seed directly plugs into the SST deployment process. So when a CDK app is waiting for CloudFormation to update your stacks, Seed pauses the build process and does this asynchronously. Thereby not charging you any build minutes for it. Thus CDK deployments on Seed are practically free!

You can [read more about this in our post here]({% link _posts/2020-09-23-fixing-cdk-deployments.md %}). Let's look at how to add a new SST app to Seed.

### Adding a New App

While adding a new app, pick the repo with your SST app in it.

![Select repo with CDK SST app](/assets/docs/adding-a-cdk-app/select-repo-with-cdk-sst-app.png)

And Seed will look for any `sst.json` files in your repo.

![Detected sst.json in repo](/assets/docs/adding-a-cdk-app/detected-sst-json-in-repo.png)

Pick the SST app you want to add. If you've got multiple SST apps or Serverless services, you can add them later.

![Adding CDK SST app](/assets/docs/adding-a-cdk-app/adding-cdk-sst-app.png)

Next, you'll be asked to [add the IAM credentials for your dev and prod environments]({% link _docs/adding-your-iam-credentials.md %}).
