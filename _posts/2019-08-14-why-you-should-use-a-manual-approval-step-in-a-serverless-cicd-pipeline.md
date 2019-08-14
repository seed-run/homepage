---
layout: post
title: Why you should use a manual approval step in a Serverless CI/CD pipeline
image: assets/social-cards/serverless-cicd-tips.png
description: In this post we'll look at why you should use a manual approval step as a part of the CI/CD pipeline for your Serverless Framework app. Since Serverless apps deploy infrastructure changes in addition to code changes, it is important to review these changes before promoting them to your production environment.
categories: tips
author: frank
---

In this post we'll look at why you should use a manual approval step as a part of the CI/CD pipeline for your Serverless Framework app.

First let's start with some background on the idea of a manual approval step. Typically, CI/CD pipelines are completely automated. This means that a Git push will trigger the CI (Continuous Integration) server to pull down your latest code and run the tests. If the tests pass, then it'll trigger your CD (Continuous Deployment) process to deploy your application. Now some teams will add a manual approval step before the deployment is done or add a step when a build is being promoted to production. The approval step is carried out by the team lead or somebody that is in charge of deployments.

To better understand why CI/CD pipelines for Serverless apps need a manual approval step, let's look at the various parts of your app that are being deployed. Starting with your code.

### Deploying code

In a traditional monolithic application (non-Serverless) development, your code mostly contains application logic. Application logic can be rolled back relatively easily and is usually side-effect free. This applies to Serverless apps as well. So while you can add a manual approval step to deployments with only code changes; you don't need to, since rollbacks work really well.

### Deploying database migrations

The deployment process gets more complicated when you have database migration scripts that get executed automatically. To handle rollbacks, you'll need to create rollback specific migration scripts. This is always tricky to do and it's not bulletproof.

Deploying database changes applies equally to Serverless and non-Serverless apps.

### Deploying infrastructure

Here is where things begin to differ between traditional non-Serverless apps and Serverless apps.

Serverless application adopt the [infrastructure as code pattern](https://serverless-stack.com/chapters/what-is-infrastructure-as-code.html), and your infrastructure definition (`serverless.yml`) sits in your codebase. When your Serverless app is deployed, the code is updated, and the infrastructure changes are applied.

A typo in `serverless.yml` could remove your resources. And in the case of a database resource, this could result in permanent data loss. There are multiple ways to prevent these problems. We have written about them here: [How to prevent accidentally deleting Serverless resources](https://seed.run/blog/how-to-prevent-accidentally-deleting-serverless-resources).

#### Infrastructure Diffs

To avoid these issues in the first place, it's recommended that you have a step to review your infrastructure changes before they get promoted to production. Just like you often do code review, an infrastructure review is also important, if not more. Luckily CloudFormation provides a feature called [Change Sets](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/using-cfn-updating-stacks-changesets.html). You give CloudFormation the new template you are going to deploy into a stack, and CloudFormation will show you the resources that are going to be added, modified and removed. You can think of it as a dry run.

We recommend generating CloudFormation Change Sets as a part of the manual approval step in your CI/CD pipeline. This will let you review the exact infrastructure changes that are going to be applied. We think this extra step can really help prevent any irreversible infrastructure changes from being deployed to your production environment mistakingly.

As an aside, CloudFormation templates and Change Sets can be pretty hard to read. Here is where Serverless Framework does a really good job of allowing to provision a Lambda and API resources in a simple and compact syntax. Behind the scene, a great number of resources are provisioned: Lambda roles, Lambda versions, Lambda log groups, API Gateway resource, API Gateway method, API Gateway deployment, just to name a few. However when CloudFormation shows you a list of changes with these resources (usually with cryptic names), it obscures the actual changes that you need to be paying attention to. This is why with Seed we've taken extra care to improve on the CloudFormation Change Set. We do this by showing changes that are relevant to the us as developers and highlight the changes that you should be paying extra attention to. You can learn more about [how Seed handles promotions here](https://seed.run/docs/promoting-to-production).
