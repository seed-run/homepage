---
layout: post
title: Cancelling Builds
author: jack
---

You can now cancel a build if it's taking too long. Seed allows you to cancel builds while they are still generating the build package (or artifacts).

![Build cancel button](/assets/blog/cancelling-builds/build-cancel-button.png)

The build process in Seed is roughly made up of two parts; the [`serverless package`](https://serverless.com/framework/docs/providers/aws/cli-reference/package/) step and the [`serverless deploy`](https://serverless.com/framework/docs/providers/aws/cli-reference/deploy/) step. If for some reason the build is taking too long to run; you can now cancel the process.

By giving you more control over the build process, Seed can help you better manage the CI/CD pipeline for your Serverless applications. You can [read more about cancelling builds in our docs]({% link _docs/cancelling-builds.md %}).
