---
layout: post
title: Update to Auto-Deploy PR Settings
categories: news
author: jack
---

Seed will now auto-deploy pull requests even if they are submitted to branches that aren't being tracked.

![New auto-deploy pull request setting](/assets/blog/update-to-auto-deploy-pr-settings/new-auto-deploy-pull-request-setting.png)

You can now specify a default stage that a PR stage should copy the settings from. This is similar to the way Seed handles [auto-deploying branches]({% link _docs/working-with-branches.md %}).

Seed will copy the following settings (if available) from the selected stage:

- IAM settings
- Post-deploy phase
- Notification settings
- Environment variables

Previously, Seed would only auto-deploy pull requests that are submitted to branches that were already being tracked. But this new setting allows Seed to auto-deploy any PR that is submitted to your repo!

Check the chapter on [working with pull requests]({% link _docs/working-with-pull-requests.md %}) in our docs for further details.
