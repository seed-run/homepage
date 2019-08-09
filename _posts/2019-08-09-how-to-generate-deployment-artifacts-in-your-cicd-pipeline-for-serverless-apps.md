---
layout: post
title: How to generate deployment artifacts in your CI/CD pipeline for Serverless apps
image: assets/social-cards/serverless-cicd-tips.png
description: In this post we'll look at generating deployment artifacts in your CI/CD pipeline for Serverless Framework apps. We'll first generate the artifacts using the `serverless package` command and then deploy it using the `--package` option in the `serverless deploy` command.
categories: tips
author: jack
---

In this post we'll look at generating deployment artifacts in your CI/CD pipeline for Serverless Framework apps.

When you think about deploying or rolling back your Serverless app, you want to treat each service as a standalone service. This means that you want to create and manage deployment artifacts for each service independently. And you want to have control over the rollback and deployment process.

Before we look at how to create a deployment artifact for a Serverless service, let's first go over how the `serverless deploy` command works internally.

### How serverless deploy works

When you run `serverless deploy`, two steps are run behind the scenes. Serverless Framework first runs `serverless package` to package your code and build a CloudFormation template. By default, the artifact is generated in the `.serverless/` directory of your project root with the following contents:

1. A zip file with the Lambda code for your service. Or a zip file for each Lambda function in your service if individual packaging is turned on.
2. A CloudFormation template file that describes the resources defined in your `serverless.yml`.
3. A `serverless-state.json` file that is used internally by Serverless Framework.

After the artifact is generated, Serverless then deploys this package by:

1. Uploading the zip file to S3.
2. Updating the CloudFormation template with S3 paths for the Lambda zip files.
3. Submitting the template to CloudFormation to kick start the deployment.

### Generating deployment artifacts

For our CI/CD pipeline we want to separate this two step process. To do this we will first do the packaging step by:

``` bash
$ serverless package --package PACKAGE_DIR
```

This will generate the aforementioned package in the `PACKAGE_DIR` directory.

We can then store this package so to reuse it later. It's a good idea to tag this package with either the Git commit that was associated with it. Or assign some other unique id that we can use later to look this up.

Once we are ready to deploy this package or if we are trying to rollback to this commit, we'll pull up the referenced package and deploy it using:

``` bash
$ serverless deploy --package PACKAGE_DIR
```

The `PACKAGE_DIR` is where the deployment artifact is stored. If you run the `serverless deploy` command with the `--package` option, it'll skip the packaging step and use the one you've provided.

This gives you control over the deployment artifacts that Serverless generates, allowing it to be better integrated into your CI/CD pipeline.
