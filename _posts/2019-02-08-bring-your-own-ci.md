---
layout: post
title: Bring Your Own CI
categories: news
author: jay
---

You can now enable Seed to trigger deployments based on the status of your CI. This can be really useful when using a service like [CircleCI](https://circleci.com) or [Travis CI](https://travis-ci.org) to run your tests.

![Connect your CI setting](/assets/blog/bring-your-own-ci/connect-your-ci-setting.png)

The **Connect Your CI** option is now publicly available and can be enabled through your app settings. You can read more about it in [our docs here]({% link _docs/connect-your-own-ci.md %}). Once enabled, Seed will wait until your CI process complete before deploying your Serverless Framework application. This ensures that you still get all the power of an external CI service, while still being able to manage your serverless deployments through Seed.
