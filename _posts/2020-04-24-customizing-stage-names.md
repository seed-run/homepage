---
layout: post
title: Customizing Stage Names
categories: news
author: jack
---

You can now customize how Seed generates the stage names for auto-deployed branches. We now have a new option in the Seed build spec that allows you to do this.

![Stage names in the Seed pipelines](/assets/blog/customize-stage-names/stage-names-in-the-seed-pipelines.png)

The stage name is central to the way Seed manages deployments and resources for your Serverless app. Seed generates it automatically for [auto-deployed branches]({% link _docs/working-with-branches.md %}). It does so by sanitizing the branch names so they work with Serverless Framework and AWS.

However, there might be cases where you might wish to customize the automatically generated stage names. For example, your team might be naming your Git branches using a `feature/feature-name` or similar pattern. But you might want to name your stages, `feature-branch`.

You can now do so using the new `stage_name_constructor` option in the `seed.yml`. This allows you to specify a small bash script to generate the stage name based on the Git branch that's being auto-deployed.

Read more about this option over on our docs on [customizing your stage names using a build spec]({% link _docs/adding-a-build-spec.md %}#customize-stage-names).
