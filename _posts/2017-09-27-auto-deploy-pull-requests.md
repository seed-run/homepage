---
layout: post
title: Auto-Deploy Pull Requests
author: frank
---

Seed now supports auto-deploying pull requests. Pull request stages allow you to preview changes before merging them.

![Pull Request Stage Building](/assets/blog/auto-deploy-pull-requests/pull-request-stage-building.png)

Here is what happens when a new pull request is submitted to your project repo.

1. Seed will check if the branch the pull request is submitted to is currently being deployed to a stage.
2. If the branch is being tracked; then a new stage is created for the submitted pull request.
3. The new PR stage will be deployed using `--stage=$STAGE`. Where `$STAGE` is the stage that is deployed using the branch from above. You can [learn more about stages in Serveress here](https://serverless-stack.com/chapters/stages-in-serverless-framework.html).
4. All the secrets from the stage is applied to the new PR stage.
5. Any new commits to the PR will be auto-deployed.

This gives you the ability to preview pull requests before merging them. You can [read more about working with pull requests in our docs]({% link _docs/working-with-pull-requests.md %}).
