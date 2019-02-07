---
layout: post
title: Git Workflow Updates
author: frank
---

We rolled out a couple of updates to improve the Git workflow support within Seed. Including auto-deploying new branches and cleaning up old PRs and branches.

![Enable auto-deploy pull request options](/assets/blog/git-workflow-updates/enable-auto-deploy-pull-request-options.png)

Seed has [supported PR based workflow]({% link _docs/working-with-pull-requests.md %}). This means that when a new PR is submitted to a branch that is tied to a stage in Seed, a new stage is created with that PR. However, these stages needed to be removed manually. We rolled out an update with an option to automatically remove these PR stages and resources once the PR is closed. You can read about it in [our docs here]({% link _docs/working-with-pull-requests.md %}#enable-auto-deploy-pull-requests).

![Enable auto-deploy new branch options](/assets/blog/git-workflow-updates/enable-auto-deploy-new-branch-options.png)

We also added support for auto deploying your app when a new branch is created. Similar to the auto-deploy PR option, Seed will automatically deploy your app to a new stage when a new branch is created. You can specify an existing stage from which to inherit the settings (environment variables or IAM credentials). Also, just like the PR options above, you can tell Seed to remove the stage once the branch is removed. You can read more about this in the chapter on [branch based workflow in our docs]({% link _docs/working-with-branches.md %}).

By better integrating with Git, Seed makes it easy to manage deployments for your Serverless Framework applications.
