---
layout: post
title: Improving the Build Logs
author: frank
---

We rolled out some major changes to the way we display the build logs in Seed. We made them more readable and added more clarity around the various build steps.

![Build logs screenshot](/assets/blog/improving-the-build-logs/build-logs-screenshot.png)

The build logs in Seed show you not just the status of your builds but it also gives you an idea of the build process and helps you debug any build errors. We made some changes to make it easier to work with the build logs.

1. Collapsable Commands

   Previously, some of the really noisy commands in the build process would drown out the rest of the build steps. We fixed this by collapsing the output of most of the commands by default. This allows you to get a sense of the entire build process at a glance.

   ![Collapsed build logs section screenshot](/assets/blog/improving-the-build-logs/collapsed-build-logs-section-screenshot.png)

2. Build Information

   We also make it clear which steps are being run as a part of the build process. For example, as a part of the `Compile` step, Seed will try to run `npm install` in your project root and service root. However, if it doesn't find a `package.json`, it'll skip these steps. The new build log makes this clear.

   ![Build logs info section screenshot](/assets/blog/improving-the-build-logs/build-logs-info-section-screenshot.png)

3. Build Hooks

   Seed allows you to customize the build process by [adding a build spec]({% link _docs/adding-a-build-spec.md %}) and hooking into the various build steps. The new build logs make it clear where a build hook will get run.

   ![Build logs hooks section screenshot](/assets/blog/improving-the-build-logs/build-logs-hooks-section-screenshot.png)

Finally, we made it a little easier to work with these pages by scrolling the entire page; instead of scrolling just a section within it.

By constantly improving the developer experience around Serverless deployments, Seed makes it easy to manage the CI/CD pipeline for your [Serverless Framework](https://serverless.com) apps.
