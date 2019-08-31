---
layout: post
title: Auto-deploy branches in GitLab and Bitbucket
categories: news
author: jack
---

We recently added support for auto-deploying branches in GitLab and Bitbucket. Previously this feature was only supported for GitHub.

![Enable auto-deploy branch setting](/assets/blog/auto-deploy-branches-in-gitlab-and-bitbucket/enable-auto-deploy-branch-setting.png)

Seed will now auto-deploy any new branches that are created in your GitLab or Bitbucket repo. You can also select a stage to copy the settings from. This means that you can configure your auto-deployed branches to use the IAM credentials, environment variables, etc. from one of your existing stages. Making it very easy to automate the workflow for your team!

You can read more about this in our docs — [**Working with branches**]({% link _docs/working-with-branches.md %}).
