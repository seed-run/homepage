---
layout: post
title: Detecting the Serverless runtime
categories: news
author: jack
---

Seed now supports automatically detecting the runtime for your Serverless services, even if they are referencing a variable in a separate YAML file. The runtime specified in your `serverless.yml` is used to figure out which build environment to use while deploying your services.

``` yaml
provider:
  name: aws
  runtime: nodejs10.x
  stage: dev
  region: us-east-1
```

Seed currently supports Node.js, Python, Go, .Net Core, and Ruby based services. And it'll pick a build environment based on the runtime your service is using.

However, if the runtime property in your `serverless.yml` is a reference, Seed was previously unable to detect it. This recent update fixes this issue. Seed will run a check before your build process to figure out the referenced runtime. It'll then automatically restart the build process with the appropriate build environment.

![Check runtime step in build logs](/assets/blog/detecting-the-serverless-runtime/check-runtime-step-in-build-logs.png)

The automatic runtime detection check only happens on your first build and only for the case where the runtime is a reference in your `serverless.yml`.

By automatically detecting the runtime, Seed ensures that your pipeline is up and running. With almost no build configuration!
