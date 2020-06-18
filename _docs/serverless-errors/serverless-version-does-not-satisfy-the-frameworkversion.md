---
layout: common-errors
title: Serverless version does not satisfy the frameworkVersion
image: /assets/social-cards/common-errors.png
description: The Serverless version (1.xx.x) does not satisfy the "frameworkVersion" (=1.xx.x) in serverless.yml
---

#### Error Message

> The Serverless version (1.xx.x) does not satisfy the "frameworkVersion" (=1.xx.x) in serverless.yml


#### Problem

Serverless Framework allows you to set a specific framework version to use for your app in the `serverless.yml`. You can read more about the `frameworkVersion` option [in the docs Serverless Framework here](https://serverless.com/framework/docs/providers/aws/guide/services#pinning-a-version). It'll use this option to deploy your app with the specified version. Note that the `frameworkVersion` can also be a range.

In the case of this error, Serverless Framework is complaining that the installed version of the framework does not match the one defined in the `frameworkVersion`.


#### Solution

You can either remove the version pinning by removing the `frameworkVersion` option from your `serverless.yml`. Or update the version of Serverless Framework by running `npm install -g serverless@x.xx.xx`.

[Seed](/) will automatically do this for you by installing the specified version in `frameworkVersion`. And in the case this isn't specified, Seed will fallback to using the latest stable version of Serverless Framework.
