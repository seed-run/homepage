---
layout: docs
title: Rolling Back
---

[Seed](/) keeps track of your builds. And the **production** build is created at the time the original build. This means that you can rollback to any of your past builds without having to rebuild your project.

> Rolling back to a past build does not rebuild your project

You can do this by going into the **Production** stage and hit **Rollback** to revert to a previous build.

![Rollback Production](/assets/docs/rolling-back/rollback-production.png)

Conceptually, rolling back is like applying a previous update on the current deployment. This means that any data removed in an update will not be restored upon rollback.

