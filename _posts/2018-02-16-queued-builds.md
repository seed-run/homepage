---
layout: post
title: Queued Builds
categories: news
author: frank
---

Seed will now automatically queue your builds if the stage is currently busy with another build.

This means that if a build is triggered while a stage is busy, it will queue the new build. And if yet another build is triggered while a build is in the queue; the previously queued build will be skipped and the new build will be queued.

If you were [running `serverless deploy`](https://serverless.com/framework/docs/providers/aws/cli-reference/deploy/) for your projects, it meant that you would need to wait for a deployment to complete before attempting another. This limits your team's ability to collaborate on your Serverless projects. Seed greatly simplifies the tooling around Serverless by managing your CI/CD pipeline with little to no configuration. 
