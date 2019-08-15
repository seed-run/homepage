---
layout: post
title: What is the right way to do rollbacks in Serverless apps
image: assets/social-cards/serverless-cicd-tips.png
description: In this post we look at what the right rollback strategy is for Serverless apps in their CI/CD pipelines. The rollback strategy for Serverless Framework apps is different because the deployment artifacts are not immutable and because the plugins are a part of the deployment process.
categories: tips
author: frank
---

Making sure that you are able to rollback your Serverless deployments is critical to managing your own CI/CD pipeline. In this post we'll look at what the right rollback strategy is for your Serverless apps.

### Background on deployment artifacts

When building a traditional application (like an Express or Rails app), you have the concept of **Immutable Artifacts**. You package the code you want to deploy and label it with a unique build id. This package then gets deployed to different environments for integration/UAT/end-to-end tests, before it gets finally deployed into the Production environment. Throughout this entire process (of progressing downstream through the pipeline), your code is packaged only once in the beginning. It happens right at the start of the pipeline when the  artifact is created; hence the **Immutable** part in Immutable Artifacts.

### Rollback for traditional Node.js applications

However, what does this mean in the context of a Node.js app? When you package the code, you run `npm install` to pull in your dependencies; you might run eslint to apply fixes; you might run Babel and Webpack to package and transpile your code. In the end you have a deployment artifact, usually a .zip file. When you need to deploy it to a given environment, you simply upload and unzip the artifact on the Node.js server. The deployment process is extremely simple.

When you need to rollback, you simply fetch the .zip artifact file from a previous build, upload and unzip. This is the preferred rollback strategy. You should avoid redeploying an older version of code. You want to make sure your rollback strategy is as robust as possible.

### Rollback for Serverless applications

Unfortunately, there are a couple of reasons why you cannot apply the above rollback strategy to [Serverless Framework](https://serverless.com) applications. Serverless Framework artifacts are not immutable. We talk about this idea [in detail in this post here]({% link _posts/2019-08-12-why-serverless-deployment-artifacts-cannot-be-reused-across-stages.md %}).

Additionally, deployment artifacts aren't the only thing that goes into a build for Serverless applications. A bit of background. Serverless Framework has created a really vibrant and collaborative community by allowing people to create plugins to simplify the development process. Plugins can inject custom actions during various points in the Serverless lifecycle. For example, the popular [serverless-webpack plugin](https://www.github.com/serverless-heaven/serverless-webpack) transpiles your code during the `serverless package` process. While another popular plugin, [serverless-domain-manager](https://www.github.com/amplify-education/serverless-domain-manager) sets up your API custom domain during the `serverless deploy` process.

This is problematic for the **Immutable** aspect of Immutable Artifacts in two ways. Here is why:

1. Plugins that inject into the deployment process can result in side-effects.
2. Serverless Framework requires **all plugins** to be installed during the deployment (ie. `serverless deploy`). Hence, even [with the deployment artifact in hand]({% link _posts/2019-08-09-how-to-generate-deployment-artifacts-in-your-cicd-pipeline-for-serverless-apps.md %}), you still need to obtain the source code and install all the plugin dependencies in order to deploy. 

### How should I rollback?

Given the above limitations. Here is how we recommend rolling back your Serverless applications.

1. [Generate deployment artifacts]({% link _posts/2019-08-09-how-to-generate-deployment-artifacts-in-your-cicd-pipeline-for-serverless-apps.md %}) for your builds.
2. Tag the artifacts with the associated commit or build id and store them.
3. When you need to rollback, make sure you are in the directory with your project source code.
4. Install all the plugin dependencies.
5. Do a `serverless deploy --package PACKAGE_DIR`, where `PACKAGE_DIR` contains the stored package from Step 1 that you want to rollback to. 

#### Summary

Rolling back in Serverless Framework applications is a little different. The artifacts cannot be used across multiple stages and the plugins are a part of the deployment process. However, with a few tweaks you can still have a robust rollback strategy in place.
