---
layout: post
title: Incremental Lambda Deploys in Beta
categories: news
image: assets/social-cards/incremental-deploys.png
author: frank
tweet: 
---

We've got an awesome new update in the works. Seed can now drastically speed up your builds by only deploying the Lambda functions that've been updated.

![Seed Incremental Deploy build log](/assets/blog/incremental-lambda-deploys-in-beta/seed-incremental-deploy-build-log.png)

### Incremental Deploys

[Incremental Deploys]({% link _docs/what-are-incremental-deploys.md %}) allows Seed to only deploy the parts of your app that have been updated. So far Seed has supported [incrementally deploying the services]({% link _docs/incremental-service-deploys.md %}) in your Serverless app. It does this by either looking at the Git log, or by using [Lerna](https://lerna.js.org) to figure out which packages have been updated.

### Incremental Lambda Deploys

Today we are launching [Incremental Lambda Deploys]({% link _docs/incremental-lambda-deploys.md %}) in beta. This allows Seed to **deploy only the Lambda functions** in your Serverless service **that've been updated**.

Seed does this by checking if the CloudFormation template or Serverless config has been changed. If it hasn't, then it'll look at the individual Lambda functions in the service and deploy only the ones that have been updated. It'll deploy the **Lambda functions concurrently and directly**, without doing a CloudFormation update. This can greatly speed up your deployments. Especially when you are actively developing your app.

By incrementally deploying your Serverless services and Lambda functions, Seed can potentially **speed up your deployments by 100x**!

> Incremental Deploys in Seed can potentially speed up your deployments by 100x!

### Enabling Incremental Lambda Deploys

To enable incremental deployments for your service, first install the [**Serverless Seed** plugin](https://github.com/seed-run/serverless-seed):

``` bash
$ npm install --save-dev serverless-seed
```

Then add it to your `serverless.yml`.

``` yml
plugins:
  - serverless-seed
```

And enable Incremental Lambda Deploys.

``` yml
custom:
  seed:
    incremental:
      enabled: true
```

And that's it. Make a couple of deployments to Seed and it'll now use this plugin to figure out if it can incrementally deploy your Lambda functions. 

You can also disable Incremental Deploys for specific stages.

``` yml
custom:
  seed:
    incremental:
      enabled: true
      disabledFor:
        - prod
```

You can [read more about Incremental Lambda Deploys over on our docs]({% link _docs/incremental-lambda-deploys.md %}).

### During the Beta 

Incremental Lambda Deploys works with most of the popular Serverless Framework plugins. But during the beta we'd like you to test it out with your setups and give us feedback. You can test it out with your apps today and [contact us via email](mailto:{{ site.email }}) or [post on our GitHub](https://github.com/seed-run/serverless-seed/issues) if you have any questions or run into any issues.
