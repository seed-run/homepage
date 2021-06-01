---
layout: post
title: Auto-deploy PRs in GitLab and Bitbucket
categories: news
author: frank
---

We recently added support for auto-deploying pull requests or merge requests in GitLab and Bitbucket. Previously this feature was only supported for GitHub.

![Enable auto-deploy PR setting](/assets/blog/auto-deploy-prs-in-gitlab-and-bitbucket/enable-auto-deploy-pr-setting.png)

Seed will now auto-deploy any new pull requests that are created in your GitLab or Bitbucket repo. You can also select a stage to copy the settings from. This means that you can configure your auto-deployed PRs to use the IAM credentials, environment variables, etc. from one of your existing stages. Making it very easy to automate the workflow for your team!

You can read more about this in our docs — [**Working with pull requests**]({% link _docs/working-with-pull-requests.md %}).
