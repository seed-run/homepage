---
layout: post
title: Free CDK Deployments in Seed
categories: news
image: assets/social-cards/cdk-sst-seed-free.png
author: jay
tweet: 
---

We've got some really exciting news to share. CDK deployments in Seed is now out of beta. And it will be **free**!

![CDK SST free build log in Seed](/assets/blog/free-cdk-deployments-in-seed/cdk-sst-free-build-log-in-seed.png)

## Background

Before we dive into the details of this announcement. Let's back up a little bit and talk about CDK and how it fits into Serverless.

[Serverless Framework](https://www.serverless.com) is great for deploying your Lambda functions. But deploying any other AWS resources requires you to write raw CloudFormation in YAML (or JSON). CloudFormation templates are incredibly verbose and even creating simple resources can take hundreds of lines of YAML.

[AWS CDK](https://serverless-stack.com/chapters/what-is-aws-cdk.html) solves this by allowing you to generate CloudFormation templates using modern programming languages. Making it truly, _infrastructure as code_. You can create resuable bits of code (or constructs) to define your infrastructure. Allowing you to easily combine and compose them. 

So you can use Serverless Framework for your Lambda functions, while using CDK for your other AWS infrastructure.

However, there are some architectural differences between CDK and Serverless Framework that makes it tricky to use them together. For example, you'll need to prefix your stack names and make sure that they are deployed to the same region and AWS account. We talk about this in detail over on Serverless Stack — [Using AWS CDK with Serverless Framework](https://serverless-stack.com/chapters/using-aws-cdk-with-serverless-framework.html).

## Serverless Stack Toolkit (SST)

To fix this, we created [**Serverless Stack Toolkit**](https://github.com/serverless-stack/serverless-stack) (SST). It enforces the same semantics as Serverless Framework, allowing you to deploy your CDK apps alongside your Serverless Framework services.

#### Stage and Region Based Deployments

So you can deploy your Lambda functions using:

``` bash
$ AWS_PROFILE=production serverless deploy --stage prod --region us-east-1
```

And use CDK for the rest of your AWS infrastructure:

``` bash
$ AWS_PROFILE=production npx sst deploy --stage prod --region us-east-1
```

#### Connecting to Serverless Framework

Once deployed, you can connect it to your Serverless Framework service in your `serverless.yml`.

``` yml
custom:
  # Our stage is based on what is passed in when running serverless
  # commands. Or falls back to what we have set in the provider section.
  stage: ${opt:stage, self:provider.stage}
  # Name of the SST app that's deploying our infrastructure
  sstApp: ${self:custom.stage}-notes-infra
```

And you can import the CloudFormation exports by using the reference to your SST app. For example, here we are importing the name of a DynamoDB table defined in CDK.

``` yml
environment:
  tableName: !ImportValue '${self:custom.sstApp}-TableName'
```

Now if you deploy your entire app (CDK and Serverless Framework) to multiple environments, it'll pick up the right set of resources automatically!

We have a detailed chapter on this as well — [Connect Serverless Framework and CDK with SST](https://serverless-stack.com/chapters/connect-serverless-framework-and-cdk-with-sst.html).

## CDK Deployments on Seed

A few weeks ago [we announced beta support for SST deployments in Seed]({% link _posts/2020-08-31-sst-deployments-beta.md %}). It features a couple of key improvements over regular CDK.

#### Concurrent Deployments

By default, CDK deploys the stacks in your CDK app one after the other. This means that CDK deployments can take a very long time. But thanks to SST, CDK stacks are deployed concurrently. And this works on Seed as well!

#### Integrated Deployment Infrastructure

We built a completely custom deployment pipeline for CDK apps. The SST deployment process is integrated into Seed. This means that the main build process doesn't have to wait for CloudFormation to deploy your stacks. Allowing us to be as efficient as possible with your deployments. In turn, **making CDK deployments free on Seed**!

We wrote a post about this where we dive into the technical details — [Fixing CDK Deployments]({% link _posts/2020-09-23-fixing-cdk-deployments.md %}).

#### Caching

We also automatically cache quite a few of the pieces of the deployments process to make sure that **Seed has the fastest CDK deployments**!

## How We Compare

So how does Seed stack up to the other CI services out there? Quite well in fact!

#### 5x Faster

If you were to deploy a simple CDK app (with 7 stacks, a few DynamoDB tables, SNS topics, and SQS queues) on CircleCI it'll take around 417 seconds. And subsequent deployments would take around 193 seconds.

On the other hand, the same CDK app with SST on Seed takes 100 seconds on the first deployment. While subsequent deployments take only 40 seconds! Thanks in part to the concurrent deployments and automatic caching.

![CDK deployments CircleCI vs Seed](/assets/blog/free-cdk-deployments-in-seed/cdk-deployments-circleci-vs-seed.png)

#### Infinitely Cheaper

And this is how much the above deployments would cost you on CircleCI vs Seed.

|                        | CircleCI | Seed            |
|------------------------|----------|-----------------|
| First deployment       |  $0.021  | Free!           |
| Subsequent deployments |  $0.012  | Still free!     |

For the above test we used a Small machine on CircleCI that requires 5 credits per minute, where 25K credits cost $15.

There are some reasonable limits on the free CDK deployments in Seed. For example, we assume that the `npm install` in your app doesn't take longer than 180s. You can [read more about this over on our docs]({% link _docs/adding-a-cdk-app.md %}#pricing-limits).

## Conclusion

[AWS CDK](https://serverless-stack.com/chapters/what-is-aws-cdk.html) is a major step up in simplifying infrastructure as code in the AWS world. [SST](https://github.com/serverless-stack/serverless-stack) now brings this to your Serverless Framework projects.

And today Seed is taking this a step further by supporting CDK SST deployments out of the box. The new integrated deployment infrastructure makes it **the fastest way to deploy your CDK apps, and it's free**!

So get started with CDK and SST:

- [Read the guide on Serverless Stack](https://serverless-stack.com/chapters/what-is-infrastructure-as-code.html)
- [Fork the sample repo and deploy it on Seed](https://github.com/AnomalyInnovations/serverless-stack-demo-api)

And let us know what you think!
