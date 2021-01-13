---
layout: docs
title: Pinning the Serverless Version
description: You can set the version of Serverless Framework you want to use for your deployments by setting it in the serverless.yml
---

Seed uses the following scheme while deciding which Serverless Framework version to use.

1. We **use a recent stable release** as a _default_ when your app or service is created. We do this because Serverless Framework releases can sometimes be buggy and these end up breaking previously working builds. We update the _default_ version every once in a while.

2. However, we **do not update previously deployed apps** with the new _default_ version. These changes only affect any newly created apps or services.

You can see the version of Serverless Framework that Seed has globally installed at the top of your builds. You can see this in the build logs as well.

![Serverless Framework version in build log](/assets/docs/pinning-the-serverless-version/serverless-framework-version-in-build-log.png)

To use a specific version of Serverless Framework for your builds you can:

#### Add it as a dependency in your `package.json`

[Starting with Serverless Framework v2](https://www.serverless.com/blog/serverless-framework-v2), it supports using the locally installed version. This means that you can add a specific version as a dependency. And Seed will use that, instead of the globally installed version.

#### Set it in your `serverless.yml`

For older versions of Serverless Framework, you can pin the version in your `serverless.yml`.

To tell Seed which version to use (for example `1.63.0`), you can set the `frameworkVersion` in the top of your `serverless.yml`.

``` yml
frameworkVersion: "1.63.0"

service: my-service

provider:
  name: aws

...
```

Alternatively, you can set a range.

``` yml
frameworkVersion: ">=1.0.0 <2.0.0"
```

Where the Serverless Framework version to be used should be in between (and including) `1.0.0` or anything less than `2.0.0`. In this case, Seed will use the highest locally cached version that matches the range.

### Caching Versions

Seed internally caches versions of Serverless Framework to speed up your builds. So if you pin your service to use a specific version, Seed will first check if it's been previously cached. If not, then it'll be added to a queue to cache it in the future.

You can read more about [version pinning in the Serverless Framework docs](https://serverless.com/framework/docs/providers/aws/guide/services#pinning-a-version).
