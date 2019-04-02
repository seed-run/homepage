---
layout: docs
title: Pinning the Serverless Version
description: You can set the version of Serverless Framework you want to use for your deployments by setting it in the serverless.yml
---

Seed uses a recent stable version of Serverless Framework. We wait until most common issues have been ironed out in a release to upgrade to it. This means that if your app relies on a newer version of Serverless Framework, you need to set it in your `serverless.yml`.

You can see the version of Serverless Framework that was used for a build in the build log page. You can see this in the build logs as well.

![Serverless Framework version in build log](/assets/docs/pinning-the-serverless-version/serverless-framework-version-in-build-log.png)

To tell Seed which version to use (for example `1.40.0`), you can set the following in your `serverless.yml`.

``` yml
frameworkVersion: "1.40.0"
```

Alternatively, you can set a range.

``` yml
frameworkVersion: ">=1.0.0 <2.0.0"
```

Where the Serverless Framework version to be used should be in between (and including) `1.0.0` or anything less than `2.0.0`.

You can read more about [version pinning in the Serverless Framework docs](https://serverless.com/framework/docs/providers/aws/guide/services#pinning-a-version).
