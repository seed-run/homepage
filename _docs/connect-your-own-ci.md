---
layout: docs
title: Connect Your Own CI
---

Seed can optionally allow you to connect to your own CI (continuous integration) service. This can be useful for cases where you have a complex set of tests or checks that need to be run before your app can be deployed. By default, Seed will deploy your app automatically on `git push` to a branch. But you can optionally tell Seed that you only want to deploy after your CI process has completed successfully.

For example, you might have Travis CI or CircleCI connected to your Git repository. If you enable the **Connect Your CI** option, then Seed will wait until the CI process has completed.

You can enable this option by heading to your app **Settings** and hitting **Connect Your CI**.

![Connect your CI setting](/assets/docs/connect-your-own-ci/connect-your-ci-setting.png)

Note that with the above option enabled, you can still manually trigger deployments through the Seed console just as before.
