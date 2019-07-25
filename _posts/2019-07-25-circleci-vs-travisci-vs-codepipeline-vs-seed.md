---
layout: post
title: CircleCI vs Travis CI vs CodePipeline vs Seed
image: assets/social-cards/seed-vs-others.png
description: In this post we'll compare the various options out there for building a CI/CD pipeline for your Serverless app. We'll be comparing CircleCI, Travis CI, CodePipeline, and Seed. We'll look at everything from ease of setup all the way to how much they cost.
categories: tips
author: frank
---

In this post we are going to do a deep comparison of the various CI/CD options for Serverless apps. We'll be comparing [CircleCI](https://circleci.com), [Travis CI](https://travis-ci.com), [CodePipeline](https://aws.amazon.com/codepipeline/), and [Seed](/).

Full disclosure, we've built Seed, so we might be a little biased towards our own service but we'll try to be as objective as possible.

If you've been following our blog, you might have come across our guides on how to build a CI/CD pipeline for real-world Serverless apps with:

- [CircleCI]({% link _posts/2019-07-09-how-to-build-a-cicd-pipeline-for-serverless-apps-with-circleci.md %})
- [Travis CI]({% link _posts/2019-07-16-how-to-build-a-cicd-pipeline-for-serverless-apps-with-travis-ci.md %})
- [CodePipeline + CodeBuild]({% link _posts/2019-07-23-how-to-build-a-cicd-pipeline-for-serverless-apps-with-codepipeline-and-codebuild.md %})

We are going to use the concepts we learnt on those posts to compare how these services stack up against each other. We'll be comparing these services across a few important criteria:

1. Ease of setup
2. Operational complexity
3. Monorepo support
4. Serverless integration
5. PR workflow support
6. Feature branch workflow support
7. Cost

Finally, we'll look at when it makes sense to use a specific service vs another.

### 1. Ease of setup

Let's start by looking at how easy it is to setup a real-world monorepo app on each of these services. You can refer to the posts that we linked above to get a sense of the process involved.

**CodePipeline**
  - HARD
  - Requires configuring multiple AWS services and tying them together. For example, you need to use [CodeBuild](https://aws.amazon.com/codebuild/) as your CI, S3 to store build cache and artifacts, CloudWatch to store build logs.
  - Usually takes 2-3 days to setup.

**Circle/Travis**
  - EASIER
  - A basic pipeline can be configured via a single buildspec.
  - The more services or environments/stages you have, the more complicated the buildspec.
  - Need to configure caching for the app and each of the services.
  - Usually takes half a day to a day to setup.

**Seed**
  - EASIEST
  - No buildspec required.
  - Auto-detects services in an app.
  - Out of the box support for environments/stages and ability to associate a stage to an AWS account.
  - A great dashboard showing the version of each service that is deployed to each stage.

### 2. Operational complexity

Once you have your CI/CD pipeline up and running, you run into cases where you need to updated it or make changes to it. For example, you might need to add a new environment or add a new service. Let's look at how these services compare when it comes to managing them.

**CodePipeline**
  - HIGH
  - Adding a new service requires updating the pipeline.
  - Setting up a new stage/environment for a new feature branch requires creating a new pipeline.

**Circle/Travis**
  - LOW
  - Adding a new service requires updating the buildspec.
  - Buildspec can be scripted to auto track new git branches.
  - Setting up new AWS account requires updating the git branch to AWS credentials mapping in the buildspec.

**Seed**
  - LOWEST
  - New service can be added through the dashboard in a couple of clicks.
  - New stages/environments can be added through a couple of clicks as well.
  - New AWS accounts can be linked through the settings with ease.

### 3. Monorepo support

Most real-world Serverless apps are made up of a few different services stored in a monorepo. Let's look at how these service stack up when it comes to working with monorepo apps.

**CodePipeline/Circle/Travis**
  - No out of the box support.
  - Need custom scripting to only deploy the services that have been updated.

**Seed**
  - Can deploy all services concurrently or [in any defined order]({% link _docs/configuring-deploy-phases.md %}).
  - Supports deploy/promote/rollback of individual services in monorepo.
  - Skips deploying services that haven't been updated.

### 4. Serverless integration

If you are looking to deploy a Serverless app, it would help to know how integrated these services are with Serverless.

**Circle/Travis**
  - Not integrated, needs a lot of manual setup and configuration.
  - Need to manually manage multiple AWS account credentials in the buildspec.

**CodePipeline**
  - Not integrated, needs a lot of manual setup and configuration.
  - Supports multi-AWS account deployment out of the box.

**Seed**
  - Deeply integrated, most Serverless Framework features and plugins work out of the box.
  - Picks the default build and deploy scripts based on the service runtime.
  - No build script required.
  - Supports multi-AWS account deployment out of the box.
  - Ability to preview CloudFormation change sets on promote.
  - Ability to view all the deployed resources.

### 5. Pull Request workflow

Most of us are familiar with the typical PR based Git workflow. Let's look at how these services support this very standard workflow.

**CodePipeline**
  - NOT SUPPORTED
  - As of writing this post, the PR workflow is not natively supported.
  - You can hack it together by using a Lambda function to listen for PR events from the Git provider and triggering the pipeline.

**Circle**
  - NOT GOOD
  - You can add some scripts to the buildspec to perform a Git merge with base branch.
  - You need to manually remove the resources in a PR stage when a PR is closed.

**Travis**
  - NOT GOOD (but better than Circle)
  - Better PR support but you still need to manually remove resources in PR stages and when a PR is closed.

**Seed**
  - FULLY SUPPORTED
  - PR workflow is natively supported without any scripting.
  - Each PR is merged with the base branch and deployed to a PR stage for preview.
  - Resources in the PR stages are auto-removed when the PR is closed.

### 6. Feature branch workflow

Also common is the practice of using feature branches while developing. Let's look at how this is supported across these services.

**CodePipeline**
  - BAD
  - You need to create a pipeline for new branches.
  - You need to manually remove resources in a stage when a branch is closed.

**Travis/Circle**
  - NOT GOOD
  - You need to manually remove resources in feature stages when a branch is closed. Meaning you'll need to handle failures as well.

**Seed**
  - FULLY SUPPORTED
  - Feature branches are auto deployed to a stage. These stages can automatically inherit the settings (environment variables, IAM credentials, etc.) from one of your other stages.
  - And all the resources in a stage get auto-removed when a feature branch is closed.

### 7. Cost

All these services have their own pricing models and it can be tricky to compare them at a glance. So it's worth taking a deeper look at them.

**Circle/Travis**
- Comparatively expensive.
- Cost scales with the number of concurrent builds.
- This means that if you are deploying a monorepo Serverless application with many services, it can get very expensive quickly.
- Or if you don't spend on concurrency, then your builds will be very slow.

**Seed**
- Cheaper than the traditional CI services.
- Cost scales with build minutes used.
- Effectively unlimited concurrency.

**CodePipeline**
- Comparatively the cheapest option.
- Uses a pay per use model.
- Effectively unlimited concurrency.

---

Now that we know how these services compare with each other. Let's get a feel for when one is a good fit for your use-case.  

#### When to use Seed
- If you have a monorepo app with multiple services.
- And the number of services in your app is growing.
- If some of your environments/stages are short-lived (ie. you are using the PR workflow or the feature branch workflow).
- You would like to have a birds-eye view of the pipeline for all the services across all stages.
- You want to review the changes before they go into production.

#### When to use CircleCI or Travis CI
- If you do not have that many environments/stages to manage. And if they don't change all that often.
- You only have 1 service per app.
- Or if you are deploying a monorepo app but paying a higher cost for concurrency isn't a concern.
- If you are using a separate solution for CD.
- Your Serverless app is a part of a large deployment system with complex test cases. Circle and Travis are great at handling tests for a variety of build environments. As an aside, we recommend using Seed in [**Connect CI**]({% link _docs/connect-your-own-ci.md %}) mode. So Seed will be a part of your larger deployment process and it'll wait for your Circle process to complete before deploying your app through Seed.

#### When to use CodePipeline
- You are all-in on the AWS approach. So you can take advantage of the consolidated billing feature. You'll get 1 bill for all your services.
- If you’re looking for a cheap CI solution,
- Or if you don't mind the setup and operational cost involved in building and maintaining your environments.

And there you have it! This post should give you a great idea of the various CI/CD options out there for your Serverless app.
