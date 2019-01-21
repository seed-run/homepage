---
layout: post
title: Enable Unit Tests
author: jack
---

We made a small tweak to the way Seed runs your unit tests. We now disable it by default for a newly created apps.

This change makes it easier for folks that are using a separate CI to run their tests. Or for the cases where you don't want to run tests as a part of the CI process.

![Unit tests disabled by default](/assets/blog/enable-unit-tests/unit-tests-disabled-by-default.png)

However, we let you know that they are being skipped and you can enable them through the app settings.

![Enable unit tests setting](/assets/blog/enable-unit-tests/enable-unit-tests-setting.png)

We want to make it easy to configure deploying your apps on Seed. And by giving you a way to control running unit tests, we think it'll help manage the CI/CD process for your [Serverless Framework](https://serverless.com) applications. You can read more about this in our docs on [running your unit tests]({% link _docs/running-tests.md %}).
