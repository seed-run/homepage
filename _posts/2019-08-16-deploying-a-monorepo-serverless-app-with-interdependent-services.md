---
layout: post
title: Deploying a monorepo Serverless app with interdependent services
image: assets/social-cards/serverless-cicd-tips.png
description: It's common for your monorepo Serverless app to have services that are dependent on each other. In this post we'll look at how the dependencies affect your deployments.
categories: tips
author: jack
---

It's common for your monorepo Serverless app to have services that are dependent on each other. In this post we'll look at how the dependencies affect your deployments.

The short version is that:
- When you introduce a new dependency in your app you cannot deploy the services concurrently.
- However, if these services have been deployed before, you can deploy them concurrently.

Let's look at why this happens. Assume our monorepo [Serverless Framework](https://serverless.com) app has the following structure.

```
/
  package.json
  libs/
  services/
    serviceA/
      serverless.yml
      handler.js
    serviceB/
      serverless.yml
      handler.js
    serviceC/
      serverless.yml
      handler.js
```

There are three services called `serviceA`, `serviceB`, and `serviceC`. Let's say `serviceA` creates an SNS topic and exports the topic's ARN in its `serverless.yml`:

``` yml
service: serviceA
...
resources:
  - Outputs:
      ATopicArn:
        Value:
          Ref: ATopic
        Export:
          Name: ATopicArn
```

And both `serviceB` and `serviceC` use the SNS topic as their Lambda triggers:

``` yml
service: serviceB
...
functions:
  handler:
    handler: handler.main
    events:
      - sns:
        'Fn::ImportValue': ATopicArn
```

### First deployment

If you are deploying the above app for the first time, you have to deploy `serviceA` first, such that the export value `ATopicArn` exists. Then deploy `serviceB` and `serviceC`. If you were to deploy all three services concurrently, `serviceB` and `serviceC` will fail with CloudFormation throwing the following error:

```
serviceB - No export named ATopicArn found.
```

It's basically saying that the ARN referenced in its `serverless.yml` does not exist. That makes sense because we haven't created it yet!

### Subsequent deployments

Once the three services have been successfully deployed, you can deploy them concurrently. This is because the referenced ARN is created after the first deployment.

### Adding new dependencies

Say you add a new SNS topic in `serviceA`, and `serviceB` and `serviceC` once again subscribe to the topic. The first deployment after the change, will again fail if all the services are deployed concurrently. You need to deploy `serviceA` first, and then deploy `serviceB` and `serviceC`.


#### Summary

And that's all there is to it! The interdependencies are created by services referencing resources that are created in another service. When you first deploy the app, make sure the service that is creating the resource is deployed first. With Seed, we handle this using the concept of [Deploy Phases]({% link _docs/configuring-deploy-phases.md %}) and to keep your builds fast, we [check if a service has been updated]({% link _docs/incremental-service-deploys.md %}).
