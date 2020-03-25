---
layout: post
title: Multi-Region Deployments
image: assets/social-cards/multi-region-deployments.png
categories: news
author: frank
---

Seed now supports deploying your Serverless app to multiple regions.

![Multiple prod stages in pipeline](/assets/blog/multi-region-deployments/multiple-prod-stages-in-pipeline.png)

We recently rolled out an update to Seed that allows you to deploy your app to multiple regions. Previously, you had to create multiple apps in Seed, connected to the same repo to get this to work.

Now you can create multiple production (or staging) stages for the same app.

![Multiple prod stages in full pipeline](/assets/blog/multi-region-deployments/multiple-prod-stages-in-full-pipeline.png)

Set them to be deployed to different regions.

![Deployed region stage setting](/assets/blog/multi-region-deployments/deployed-region-stage-setting.png)

And voila! Your app is now available in multiple regions. For further details, head over to our docs on [multi-region deployments]({% link _docs/multi-region-deployments.md %}).
