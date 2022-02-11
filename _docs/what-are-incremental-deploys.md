---
layout: docs
title: What are Incremental Deploys
---

Incremental Deploys allow Seed to only deploy the parts of your app that have been updated. Serverless apps are typically made up of multiple services. And each service is made up of multiple Lambda functions.

Incremental Deploys work on both the service and Lambda function level. This means that Seed will check the following before doing a deployment:

1. Has the service that needs to be deployed been updated?
2. Which specific Lambda functions in this service need to be deployed?

> Incremental deploys in Seed can potentially speed up your Serverless deployments 100x

These two checks allow Incremental Deploys to potentially speed up your Serverless deployments by 100x!

### Incremental Service Deploys

When you trigger a deployment for your Serverless app, Seed will try to deploy each of your services concurrently (or according to [the Deploy Phases that you've configured]({% link _docs/configuring-deploy-phases.md %})).

To check if a service has been updated, Seed uses the **Git log** (check if the files in a service have been updated), [**Lerna**](https://lerna.js.org), or [**pnpm**](https://pnpm.io) (check which packages have been updated).

[Read more about how Seed deploys only the services that've been updated <i class="fa fa-arrow-right" aria-hidden="true"></i>]({% link _docs/incremental-service-deploys.md %})

### Incremental Lambda Deploys

While deploying a service, Seed will check if the CloudFormation template or Serverless config has been changed. If it hasn't, then it'll look at the individual Lambda functions in the service and deploy only the ones that have been updated. It'll deploy the Lambda functions concurrently and directly, without doing a CloudFormation update.

[Read more about how Seed deploys only the Lambda functions that've been updated <i class="fa fa-arrow-right" aria-hidden="true"></i>]({% link _docs/incremental-lambda-deploys.md %})

