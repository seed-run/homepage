---
layout: docs
title: Cancelling Builds
---

There are cases when something might go wrong while running a build and you might want to manually stop or cancel it. Seed allows you to cancel a build while it is in progress.

You can do this by hitting **Cancel** on the stage that the build is running in.

![Cancel build in pipeline](/assets/docs/cancelling-builds/cancel-build-in-pipeline.png)

You can also click through to the build in question and hit **Cancel Build**.

![Cancel build in build report](/assets/docs/cancelling-builds/cancel-build-in-build-report.png)

This will cancel the build in progress. Note that, while Seed can cancel the build process for you, it cannot control the state of the deployed resources for the cancelled build.
