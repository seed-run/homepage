---
layout: post
title: Saving build minutes for monorepo apps
categories: news
author: jay
tweet: 
---

We are making a small but critical update to help save you build minutes while deploying your monorepo Serverless app.

![No build minutes charged in Seed](/assets/blog/saving-build-minutes-for-monorepo-apps/no-build-minutes-charged-in-seed.png)

Seed does a great job of only deploying the services that've been updated in your monorepo Serverless app. This really speeds up your deployments and saves you build minutes. We do this by [checking your Git log for updates]({% link _docs/deploying-monorepo-apps.md %}#check-the-git-log-for-updates). Or [using Lerna to check for updates]({% link _docs/deploying-monorepo-apps.md %}#use-lerna-to-check-updated-packages) (if you are using Lerna + Yarn Workspaces).

However, these checks can take 10-20 seconds to run (depending on the size of the repo), rounding up to 1 build minute. This can really add up if you have a dozen services in your app.

Today we are rolling out a change to make these checks free. This means that **you won't be charged for any build minutes if a service in your app hasn't been updated**.

We [are constantly trying to ensure](https://twitter.com/jayair/status/1258092217383731201?s=20) that our pricing is as fair and transparent as possible. To learn more about our pricing plans, visit — [{{ site.url | replace: "https://", "www." | replace: "http://", "www." }}](/pricing)
