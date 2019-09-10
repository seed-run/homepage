---
layout: post
title: Problems with Serverless version updates
categories: news
author: frank
---

We've got a quick update on some of the recent issues our users experienced with the latest Serverless Framework version upgrade.

Recently we update the default Serverless Framework version that Seed uses from `1.40.0` to `1.51.0`. This caused a couple of problems for our users:

1. The latest AWS SDK version (that Serverless Framework internally uses) was faulty. This was causing `serverless deploy` to fail. This was happening because Serverless Framework uses `"aws-sdk": "^2.518.0"` as a dependency and there was a problem with AWS SDK `2.525.0`.

2. The `serverless package` command seems to hang on the `Serverless: Invoke aws:common:moveArtifactsToPackage` step for some users. It's unclear what was causing this issue but it appears as though this has been broken since `1.48.1`. 

To deal with the first issue, we rolled out a hotfix to internally force Serverless Framework to use a stable AWS SDK version. While we are still investigating the second issue, we rolled back the default version to `1.40.0`.

A quick background on the default version that Seed uses.

#### Why Seed uses an older Serverless Framework version

If you've built a service with Seed, you'd have noticed that Seed uses an older version of Serverless Framework by default. The reason we do this is because newly released Serverless Framework versions often break. This causes your builds to suddenly fail, even though you would've not made any significant changes on your end.

![Serverless Framework version in build log](/assets/blog/problems-with-serverless-version-updates/serverless-framework-version-in-build-log.png)

To avoid this, Seed will continue using an older stable version of Serverless Framework for your builds. And once we feel confident (after testing) about a newer version we decide to roll it out as the default.

You can override this by picking the version you want to use in your `serverless.yml`. By pinning the version, Seed will use that specific version for your build. You can read our doc on [pinning the Serverless version here]({% link _docs/pinning-the-serverless-version.md %}).

In this case, we tested `1.51.0` and decide to upgrade to it. However, we were unable to catch the issue we highlighted above.

#### Moving forward

To prevent such issues from happening, we are going to be implementing a new policy for Serverless Framework version upgrades.

1. We will continue to default to using an older stable Serverless Framework version that **we've tested internally**.

2. However, when we update the default version, it'll only take effect for any **new** services or apps. This means that if your app was deploying successfully before, it'll continue to do so.

3. If you want to use a newer version than the one Seed is using, we recommend **specifying it** in your `serverless.yml`. Refer to our [doc on how to do this]({% link _docs/pinning-the-serverless-version.md %}).

4. Seed currently caches versions of Serverless Framework internally to speed up your builds. If the version you've selected is not cached, Seed will add it to a job queue to have it cached for your future builds.

We are hoping these changes ensure that you are not affected by any issues with new Serverless Framework version updates.
