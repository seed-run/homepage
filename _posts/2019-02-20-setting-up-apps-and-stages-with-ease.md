---
layout: post
title: Settings up Apps & Stages with Ease
author: jack
---

We've made it a lot more easier to add and configure new apps and stages in Seed. Now you can inherit the settings from an existing app or stage.

![Inherit app settings for a new app](/assets/blog/setting-up-apps-and-stages-with-ease/inherit-app-settings-for-a-new-app.png)

We know once you fall in love with Serverless, you can end up creating a ton of Serverless apps. However, it can be a pain to configure these over and over again. For example, you need to configure the IAM settings, the stages, the environment variables per stage, etc. for every new app you create. This can be a really tedious and sometimes error prone process.

Today we pushed out an update to address this. Now when you try to add a new app, you can simply choose an existing app to inherit the settings from. Seed will copy over the settings while creating the new app. And don't worry, you can always tweak these later. You can read more about [adding an app here]({% link _docs/index.md %}).

We do something similar when you add a new stage. You can select an existing stage to inherit the settings from.

![Inherit stage settings for a new stage](/assets/blog/setting-up-apps-and-stages-with-ease/inherit-stage-settings-for-a-new-stage.png)

You can read more about [adding a stage here]({% link _docs/adding-a-stage.md %}). By making it easier to configure your apps and stages, Seed makes it really easy to manage deployments for your Serverless Framework projects.
