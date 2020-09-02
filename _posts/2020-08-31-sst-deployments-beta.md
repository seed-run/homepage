---
layout: post
title: SST Deployments Beta
categories: news
image: assets/social-cards/serverless-stack-toolkit.png
author: frank
tweet: https://twitter.com/SEED_run/status/1301149215083692033
---

We've got an exciting announcement. Seed now supports deploying [AWS CDK](https://aws.amazon.com/cdk/) alongside your [Serverless Framework](https://www.serverless.com/) services, thanks to [SST](https://github.com/serverless-stack/serverless-stack).

![SST build log in Seed](/assets/blog/sst-deployments-beta/sst-build-log-in-seed.png)

### Background

[Serverless Framework](https://www.serverless.com) is great for deploying your Lambda functions. But deploying any other AWS resources requires you to write a lot of CloudFormation in YAML. CloudFormation templates are incredibly verbose and even creating simple resources can take hundreds of lines of YAML. [AWS CDK](https://aws.amazon.com/cdk/) solves this by allowing you to generate CloudFormation templates using modern programming languages. Making it truly, _infrastructure as code_.

### Introducing SST

However, there are some architectural differences between CDK and Serverless Framework that makes it tricky to use them together. For example, you'll need to prefix your stack names and make sure that they are deployed to the same region and AWS account.

To fix this, we created [Serverless Stack Toolkit](https://github.com/serverless-stack/serverless-stack) (SST).

So you can deploy your Lambda functions using:

``` bash
$ AWS_PROFILE=production serverless deploy --stage prod --region us-east-1
```

And use CDK for the rest of your AWS infrastructure:

``` bash
$ AWS_PROFILE=production npx sst deploy --stage prod --region us-east-1
```

### Turbocharged Deployments

We've also created a completely **new deployment infrastructure** in Seed. Making it the fastest possible way to deploy your SST apps! This features:

- Build servers that start deployments **instantly**
- Deploying all your CloudFormation stacks **concurrently**
- And **not wasting build minutes** waiting for CloudFormation to update

This means that SST apps are deployed **incredibly fast**. And since you are not charged while waiting for CloudFormation to complete, deployments will be **practically free**!

As an example, a simple AWS CDK app with 7 stacks (a few DynamoDB tables, SNS topics, and SQS queues), deployed on CircleCI takes 417 seconds. While on Seed it takes 100 seconds. And subsequent deployments take 193 seconds on CircleCI vs. 40 seconds on Seed!

### Getting Started

We'd like you to give SST a try and to send us your feedback.

1. Fork the sample repo — [github.com/serverless-stack/serverless-stack-resources-sample](https://github.com/serverless-stack/serverless-stack-resources-sample)
2. Add it to [Seed](https://console.seed.run)
3. Deploy it

Also, make sure to check out the docs and star the SST repo — [**github.com/serverless-stack/serverless-stack**](https://github.com/serverless-stack/serverless-stack)

SST deployments during the beta are free. So try it out and [let us know what you think](mailto:{{ site.email }})!
