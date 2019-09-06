---
layout: post
title: Auto-remove stage improvements
categories: news
author: jack
---

We've made a few changes to make the process of auto-removing stages far more stable and robust.

![Seed auto-remove stage on PR close](/assets/blog/auto-remove-stage-improvements/seed-auto-remove-stage-on-pr-close.png)

Stages in Seed can be automatically removed when you close a PR or delete a branch. However if the removal process fails, you might end up with a large number of these half-removed stages in your Seed dashboard. Seed allows you to manually remove these stages but we want to try and make sure that the removal process is as robust as possible.

We are rolling out a couple of improvements to make this happen:

- Remove the services in the correct order

  The biggest change in this update affects monorepo Serverless apps [with service dependencies]({% link _docs/configuring-deploy-phases.md %}). Seed will now remove your services in the **reverse** order. For example assume your services; `serviceA`, `serviceB`, and `serviceC` are deployed in the following order: `serviceA` > `serviceB` > `serviceC`. When a stage is removed, they'll be removed in reverse; `serviceC` > `serviceB` > `serviceA`. This is to handle the case where a service might be referencing a resource from one that was deployed before it. 

- Double-check the stack removal

  Sometimes the `serverless remove` command returns a success status even though the removal fails. In this case the stage will be marked as failed to remove. This specifically happens when a stack has an export value that is in use by another service. Serverless Framework marks the removal as a success even though CloudFormation fails to remove the stack.

- General stability related fixes

We hope these changes fix most of the auto-remove issues that people are running into. Making this process robust is necessary to fully automate [a PR based development workflow]({% link _docs/working-with-pull-requests.md %}) for Serverless apps.
