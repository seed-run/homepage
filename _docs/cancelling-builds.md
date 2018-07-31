---
layout: docs
title: Cancelling Builds
---

There are cases when something might go wrong while running a build and you might want to manually stop or cancel it. Seed allows you to cancel a build **before it starts deploying**.

The [build process has two parts]({% link _docs/generating-trusted-builds.md %}); creating the build package (or artifacts) and then deploying those artifacts. You can cancel a build while it is still in the process of generating the artifacts.

![Build cancel button](/assets/docs/cancelling-builds/build-cancel-button.png)

Once the deployment process starts you cannot cancel the build since AWS is creating the resources.
