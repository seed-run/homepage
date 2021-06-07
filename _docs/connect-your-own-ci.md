---
layout: docs
title: Connect Your Own CI
---

Seed can optionally allow you to connect to your own CI (continuous integration) service. This can be useful for cases where you have a complex set of tests or checks that need to be run before your app can be deployed. Or if your Serverless app needs to be deployed as a part of your existing infrastructure. By default, Seed will deploy your app automatically on `git push` to a branch. But you can optionally tell Seed that you only want to deploy after your CI process has completed successfully.

We currently support the _Connect Your CI_ option for **GitHub** and **Bitbucket**. [Contact us](mailto:{{ site.email }}) if you'd like to use it for GitLab. Note, you can also use the [Seed CLI]({% link _docs/deploying-with-the-seed-cli.md %}) to trigger deployments.

You can enable this option by heading to your app **Settings** and enable **Connect Your CI**.

![Connect your CI setting](/assets/docs/connect-your-own-ci/connect-your-ci-setting.png)

Let's look at how this setting works in detail.

### GitHub

Seed integrates with the [GitHub Checks API](https://developer.github.com/v3/checks/) to connect to your CI. The following services are supported:

1. [GitHub Actions](https://github.com/features/actions)
2. [Travis CI](https://travis-ci.com)
3. [CircleCI](https://circleci.com): By default, CircleCI does not enable GitHub Checks. You can enable this from your CircleCI settings — [circleci.com/docs/2.0/enable-checks/](https://circleci.com/docs/2.0/enable-checks/).

When the _Connect Your CI_ option is enabled for GitHub, Seed will:

- Listen for the [Check Suite](https://developer.github.com/v3/checks/suites/) to complete successfully,
- And ensure that it was either triggered by GitHub Actions, Travis CI, or Circle CI.

### Bitbucket

For Bitbucket, Seed relies on the commit status. CI services like Travis CI or CircleCI update the commit status after their build process. So if you enable the _Connect Your CI_ option, then Seed will wait until the CI process has completes and updates the commit status.

Note that with the above option enabled, you can still manually trigger deployments through the Seed console just as before.
