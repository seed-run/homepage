---
layout: post
title: Updating the build image your service uses
categories: news
author: jack
tweet: https://twitter.com/SEED_run/status/1308395386843918336
---

We rolled out an update to the [Seed console]({{ site.console_url }}) to allow you to change the build image that your Serverless services use.

![Build image options in Seed service settings](/assets/blog/updating-the-build-image-your-service-uses/build-image-options-in-seed-service-settings.png)

Seed will automatically select the appropriate build image for your Serverless service. It does this based on the runtime of your service. You can check out the build images that we use here — [Seed Build Images]({% link _docs/seed-build-images.md %})

However, Seed will not update the build image if you were to change the runtime of the service. This is because we don't want to affect any scripts that you might've been running.

To fix this, Seed now gives you the option to update the build image that your service is currently using. You can find this in the service's settings. [Read more about this setting over on our docs]({% link _docs/seed-build-images.md %}#changing-the-build-image).
