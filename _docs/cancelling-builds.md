---
layout: docs
title: Cancelling Builds
---

There are cases when something might go wrong while running a build and you might want to manually stop or cancel it. Seed allows you to cancel a build while it is in progress.

You can do this by heading over to the build page while it is in progress. For example, here we select build `v3` in the `pr2` stage.

![Select in progress build](/assets/docs/cancelling-builds/select-in-progress-build.png)

And hit **Cancel Build**.

![Build cancel button](/assets/docs/cancelling-builds/build-cancel-button.png)

This will cancel the build in progress. Note that, while Seed can cancel the build process for you, it cannot control the state of the deployed resources for the cancelled build.
