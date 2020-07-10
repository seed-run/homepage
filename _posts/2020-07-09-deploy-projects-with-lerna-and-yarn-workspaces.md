---
layout: post
title: Deploy Projects with Lerna and Yarn Workspaces
categories: news
author: frank
image: assets/social-cards/lerna-and-yarn-workspaces.png
---

Seed can now use [Lerna](https://lerna.js.org) + [Yarn Workspaces](https://classic.yarnpkg.com/en/docs/workspaces/) to only deploy the services that have been updated in your Serverless app.

Lerna and Yarn Workspaces allow you to manage packages and dependencies in a monorepo architecture. And since most large Serverless apps are monorepo projects with multiple services; it's a perfect fit!

If you are using this setup, just add the following to your `seed.yml`:

``` yml
check_code_change: lerna
```

And Seed will use Lerna to figure out which of your services have been updated. This works better than the default Git log check that Seed uses. Since Lerna keeps track of the dependencies between the packages in your repo, it can better detect if a service has been updated. In contrast, the [Git log check]({% link _docs/deploying-monorepo-apps.md %}#check-the-git-log-for-updates) uses the directory structure to see if a service has been updated. This check usually leads to more false positives.

You can read more about these checks in detail in the [Deploying Monorepo Apps]({% link _docs/deploying-monorepo-apps.md %}) chapter in our docs.

We also wrote about the Lerna + Yarn Workspaces setup over on [Serverless Stack](https://serverless-stack.com/), in the [Using Lerna and Yarn Workspaces with Serverless](https://serverless-stack.com/chapters/using-lerna-and-yarn-workspaces-with-serverless.html) chapter. And we created a starter project to help you get started — [**Serverless Lerna + Yarn Workspaces Monorepo Starter**](https://github.com/AnomalyInnovations/serverless-lerna-yarn-starter)
