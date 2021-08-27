---
layout: post
title: Build machine options for SST apps
categories: news
author: frank
---

SST apps on Seed can now be deployed using any [build machine]({% link _docs/build-machine-types.md %}) or [build image]({% link _docs/seed-build-images.md %}).

![SST build options in Seed](/assets/blog/build-machine-options-for-sst-apps/sst-build-options-in-seed.png)

Previously, [SST (and CDK) apps]({% link _docs/adding-a-cdk-app.md %}) could only be deployed with a single build machine and build image. Now SST apps are supported for all the build machine options.

You might recall, SST apps deploy for free on Seed. They are still free for [Standard build machines]({% link _docs/build-machine-types.md %}). For the larger build machines, you'll be charged for the time it takes to build your app. But not for the time it takes for CloudFormation to update your app.

You can [read more about the pricing details here]({% link _docs/adding-a-cdk-app.md %}#pricing-limits).
