---
layout: post
title: How to handle service dependencies when rolling back a monorepo Serverless app
image: assets/social-cards/serverless-cicd-tips.png
description: In this post we'll look at the rollback strategy you should use in your CI/CD pipeline for monorepo Serverless Framework apps. We look at the various scenarios and come up with a robust strategy that works across all cases.
categories: tips
author: frank
---

In a Serverless app with a single service, the rollback strategy in your CI/CD pipeline simply involves re-deploying the previously packaged deployment artifact.

However, in a monorepo setup, your app is made up of many [Serverless Framework](https://Serverless.com) services. There might be services that are dependent on each other. These dependencies require the services to be deployed in a specific order. We have [a post outlining how to deploy monorepo Serverless apps with interdependent services here]({% link _posts/2019-08-16-deploying-a-monorepo-serverless-app-with-interdependent-services.md %}). This same order also needs to be followed when rolling back deployments.

In this post we are going to cover all the possible rollback scenarios for a monorepo Serverless app with service interdependencies. We'll use this to come up with a strategy that you can apply in your CI/CD pipeline.

Let's consider the following monorepo setup as an example. The app has two Serverless Framework services, located inside the `services/` directory.

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
```

Now let's take a look at the three rollback scenarios.

### 1. Rollback an update that added an inter-service dependency

Say you added an SNS topic named `ATopic` in ServiceA and exported the topic's ARN. Here is an example of ServiceA's `serverless.yml`:

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

And ServiceB imports the topic and uses it to trigger the `topicHandler` function:

``` yml
service: serviceB
...
functions:
  topicHandler:
    handler: handler.main
    events:
      - sns:
        'Fn::ImportValue': ATopicArn
```

You commit the changes and deploy the services. Note that ServiceA had to be deployed first. This is to make sure that the export value `ATopicArn` exists, and then we deploy ServiceB.

Assume that after the services have been deployed, your Lambda functions start to error out and you have to rollback.

In this case, you need to: **rollback the services in the reverse order of the deployment**.

Meaning ServiceB needs to be rolled back first, such that the exported value `ATopicArn` is not used by other services, and then rollback ServiceA to remove the SNS topic along with the export.

### 2. Rollback an update that removed an inter-service dependency

Let's use a similar example. Say ServiceA exported `ATopicArn`. And it is imported by ServiceB. And you decide to remove the topic. This time around ServiceB has to be deployed first, such that the exported value `ATopicArn` is not used, and then deploy ServiceA.

Assume that after the services were deployed, you have to rollback. In this case as well, you need to: **rollback the services in the reverse order of the deployment**.

Meaning ServiceA needs to be rolled back first, to make sure that the export value `ATopicArn` exists, and then rollback ServiceB.

### 3. Rollback an update that did not update inter-service dependency

This is the case when you made only code changes to your services. This is likely to be most of your commits. The deployment strategy here is straight forward. You can deploy all of your services concurrently. And when you need to rollback, you can simply: **rollback the services in any order**.

#### Summary

Now that we've covered all the possible rollback scenarios, it should be clear that the best strategy for your Serverless CI/CD pipeline is to **always rollback the services in the order in which they were deployed**. You can apply this regardless of the type of changes that were made, whether you were adding a dependency or removing it!
