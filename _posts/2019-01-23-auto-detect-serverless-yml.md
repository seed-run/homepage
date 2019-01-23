---
layout: post
title: Auto-Detect Serverless.yml
author: jack
---

Seed will now automatically detect the `serverless.yml` file in your project.

![Auto-detect serverless.yml adding app](/assets/blog/auto-detect-serverless-yml/auto-detect-serverless-yml.png)

We rolled out a neat little change to make it easier to add your [Serverless Framework](https://serverless.com) apps and services to Seed. We will automatically check for a `serverless.yml` in your repo while adding an app. We also parse the YAML file for the name of your service.

We do something similar when you are adding additional services.

![Detect serverless.yml adding app](/assets/blog/auto-detect-serverless-yml/detect-serverless-yml-add-service.png)

With Seed we are making it as easy as possible to configure a CI/CD pipeline for your Serverless Framework apps on AWS.
