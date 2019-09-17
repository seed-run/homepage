---
layout: post
title: Changes to how environment variables are stored
image: assets/social-cards/environment-variables.png
categories: news
author: frank
---

We are rolling out some changes to the way environment variables are stored on Seed. In this post we'll look at what is being changed and how the changes are being rolled out.

### What is being changed

Previously, environment variables on Seed were stored on our end after being encrypted using your [AWS KMS keys](https://aws.amazon.com/kms/). However, we've run into a few issues with this:

1. The AWS permissions needed to do this are fairly expansive. We needed nearly complete access to KMS to create a key and use it.

2. And in many cases teams would opt to not give KMS access. Instead allowing Seed to encrypt and decrypt on our end.

3. Additionally, if you were using multiple AWS accounts for your stages and ended up changing the credentials for the stage, Seed would not be able to decrypt the environment variables anymore.

To fix these issues, we are now moving away from asking for access to your KMS and instead encrypting it completely on our end using our KMS credentials.

### How are these changes being rolled out

Like most changes that we make to the Seed build process, it's being rolled out in phases.

1. These changes go into effect immediately for any newly created apps.

2. For existing apps, we'll be switching them over on Sep 23rd, 2019. You should not notice any changes to your deployments.

Note that these changes only apply to the environment variables that you choose to have stored on Seed. These typically include things like credentials that are needed in the build process. For secrets that are used in your app, we recommend using [AWS Parameter Store](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-parameter-store.html). We've written about this in one of our Serverless Tips posts — [How to manage secrets for your Serverless app]({% link _posts/2019-07-03-how-to-manage-secrets-for-your-serverless-app.md %}).

If you have any questions about these changes, feel free to [contact us via email](mailto:{{ site.email }}).
