---
layout: post
title: How to structure a real-world monorepo Serverless app
image: assets/social-cards/serverless-monorepo.png
description: In this post we look at how to organize monorepo Serverless Framework apps in detail. We'll also look at how to share common code and config and how to structure the serverless.yml file.
categories: tips
author: frank
---

Serverless applications are usually made up of multiple services and they are typically organized in a [monorepo](<https://en.wikipedia.org/wiki/Monorepo). In this post we are going to look at how to structure a real-world monorepo Serverless app.

As your Serverless app starts to grow, you start adding new services and organizing your app. We have [a great series on this over on Serverless Stack](https://serverless-stack.com/chapters/organizing-serverless-projects.html). However there are a few details those chapters and a lot of the other articles on the web do not cover.

This post will attempt to answer the following questions:

1. Do I use one or multiple `package.json` files?
2. How do I share common code and config between services?
3. How do I share common config between the various `serverless.yml`?
4. How do I reference resources across services?
5. How do I automate deployments for services that depend on other services?

We are looking at Node.js for this post, put the concepts roughly apply to other languages as well.

### Let's look at an example

Let's use a real-world example for the purpose of this post. Imagine that you are running an online store, and when a customer makes a purchase, you need to process the payment. Once the payment goes through, you'll send out a confirmation email and start the shipping process at the same time. To facilitate this, we are going to build a Serverless app with:

- An API service that processes the payment. If the payment goes through, it'll publish a `PURCHASED` message.
- A service that listens for the `PURCHASED` message and sends out the confirmation email.
- A service that also listens for the `PURCHASED` message and creates a shipping record in the database.

The code structure will look something like this:

```
/
  package.json
  config.yml
  libs/
  services/
    purchase-api/
      package.json
      serverless.yml
      handler.js
    confirmation-job/
      serverless.yml
      handler.js
    shipping-job/
      serverless.yml
      handler.js
```

We'll go over the details below. But you can find the source used in this post here - [https://github.com/seed-run/serverless-example-monorepo-with-code-sharing](https://github.com/seed-run/serverless-example-monorepo-with-code-sharing).

### 1. Structuring the package.json

The first question you typically have is about the `package.json`. Do I just have one `package.json` or do I have one for each service? We recommend having multiple `package.json` files.

We use the `package.json` at the project root to install the dependencies that will be shared across all the services. For example, the [serverless-bundle](https://github.com/AnomalyInnovations/serverless-bundle) plugin that we are using to optimally package our Lambda functions is installed at the root level. It doesn't make sense to install it in each and every service.

On the other hand, dependencies that are specific to a single service are installed in the `package.json` for that service. In our example, the `purchase-api` service uses the `stripe` NPM package. So it's added just to that `package.json`.

This setup implies that when you are deploying your app through a CI; you'll need to do an `npm install` twice. Once in the root level and once in a specific service. [Seed](/) does this automatically for you.

Usually, you might have to manually pick and choose the modules that need to be packaged with your Lambda function. Simply packaging all the dependencies will increase the code size of your Lambda function and this leads to longer cold start times. However, in our example we are using the `serverless-bundle` plugin that internally uses [Webpack](https://webpack.js.org)'s tree shaking algorithm to only package the code that our Lambda function needs.

### 2. Sharing common code and config

The biggest reason you are using a monorepo setup is because your services need to share some common code, and this is the most convenient way to do so.

Alternatively, you could use a multi-repo approach where all your common code is published as private NPM packages. However, it does add an extra layer of complexity and doesn't make sense if you are a small team just wanting to share some common code.

In our example, we want to share some common config code. We'll be placing these in a `libs/` directory. Our services need to make calls to various AWS services using the AWS SDK. And we are going to put the SDK configuration code in the `libs/aws-sdk.js` file.

``` js
import AWS from 'aws-sdk';

AWS.config.update({
  httpOptions: {
    timeout: 5000,
  }
});

export default AWS;
```

Our Lambda functions will now import this instead of the standard AWS SDK.

``` js
import AWS from '../../libs/aws-sdk';
```

The great thing about this is that we can easily change any AWS related config and it'll apply across all of our services.

### 3. Share common serverless.yml config

We have separate `serverless.yml` configs for our services. However, we end up needing to share some config across all of our `serverless.yml` files. To do that:

- Place the shared config values in a common yaml file at the root level.
- And reference them in your individual `serverless.yml` files.

Let's assume for our example we want to set the timeout for our Lambda functions to 20 seconds across all the services. Start by creating a `config.yml` at the project root.

``` yml
timeout: 20
```

And use the config in your service's `serverless.yml`:

``` yml
...

provider:
  name: aws
  timeout: ${file(../../config.yml):timeout}

...
```

You can do something similar for any other `serverless.yml` config that needs to be shared.

### 4. Reference resources in other services

In the `purchase-api`, we created an SNS topic. For the `confirmation-job` and `shipping-job` services to be able to subscribe to this topic, the `purchase-api` needs to export the ARN of the topic. To do this, we need to add the following to the `serverless.yml` of the `purchase-api`.

```yml
...

resources:
  Resources:
    PurchasedTopic:
      Type: AWS::SNS::Topic
      Properties:
        TopicName: ${opt:stage}-purchased

  Outputs:
    PurchasedTopicArn:
      Value:
        Ref: PurchasedTopic
      Export:
        Name: ${opt:stage}-PurchasedTopicArn
```

And in the `serverless.yml` of the other two job services, add the following:


```yml
...

functions:
  handler:
    handler: handler.main
    events:
      - sns:
        'Fn::ImportValue': '${opt:stage}-PurchasedTopicArn'
```

Note that we are using `${opt:stage}` here because we want to parameterize our resources using the name of the stage we are deploying to.

### 5. Deploying with service dependencies

In our example, the two job services are dependent on the `purchase-api` service. This means that there is an order in which our services need to be deployed. You first need to deploy the `purchase-api` service. This will generate the ARN of the SNS topic that we can then reference. Just make sure that the deployment script in your CI/CD pipeline handles this.

In [Seed](/) you can do this easily by configuring [Deploy Phases]({% link _docs/configuring-deploy-phases.md %}). You can set it to deploy the `purchase-api` service first and then concurrently deploy the two job services.

#### Summary

This post should give you a good idea of how to structure a real-world monorepo Serverless app. To quickly summarize what we covered:

- Common code always sits at a level above the services.
- A code or config change above the level of the services will affect ALL the services.
- A code or config change at the level of the service ONLY affects that specific service.
- In a CI/CD environment like Seed that supports monorepo natively; following this structure means that when something changes in a service, only that service will be deployed. For example, the `purchase-api` does not need to be deployed if a commit only contains changes in the `shipping-job` service directory.

And that should do it! Make sure to check out [the sample repo that was used in this post](https://github.com/seed-run/serverless-example-monorepo-with-code-sharing). It should give you a great setup as your Serverless apps as they grow. 
