---
layout: post
title: Redeploy the latest build
categories: news
author: frank
---

Seed now allows you to redeploy the latest build. You can find this new button in the build detail page.

![Seed redeploy build](/assets/blog/redeploy-the-latest-build/seed-redeploy-build.png)

Now, if you head over to the latest build in a stage, you can redeploy it. This will do a [force deploy]({% link _docs/manually-deploying.md %}#force-deploys) to that stage with the commit used for that build.

This is useful for cases where you updated an environment variable (an SSM variable, or something external that the build depends on) and you need to redeploy it. Now you can simply hit redeploy without having to do push a commit to trigger a deployment.
