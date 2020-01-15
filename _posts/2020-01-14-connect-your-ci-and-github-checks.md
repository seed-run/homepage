---
layout: post
title: Connect your CI and GitHub Checks
categories: news
author: jack
---

We recently rolled out an update to the _Connect Your CI_ option on Seed to support GitHub Checks.

![Connect your CI setting](/assets/blog/connect-your-ci-and-github-checks/connect-your-ci-setting.png)

Seed allows you to connect your own CI service. This can be useful when your Serverless deployments need to be triggered after a complex suite of tests and checks complete successfully. This recent update integrates with [GitHub Checks API](https://developer.github.com/v3/checks/).

![GitHub Checks CircleCI](/assets/blog/connect-your-ci-and-github-checks/github-checks-circleci.png)

Seed now supports [GitHub Actions](https://github.com/features/actions), [Travis CI](https://travis-ci.com), and [CircleCI](https://circleci.com). Make sure to [**check out our docs**]({% link _docs/connect-your-own-ci.md %}) for further details.

By allowing you to connect your CI, Seed makes it easy to manage your Serverless deployments with your existing infrastructure.
