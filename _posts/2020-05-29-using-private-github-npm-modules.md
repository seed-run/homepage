---
layout: post
title: Using private GitHub npm modules
categories: tips
author: jack
---

In this post we'll look at how to make sure Seed is deploying your Serverless services with your private GitHub npm modules.

![GitHub Packages homepage](/assets/blog/using-private-github-npm-modules/github-packages-homepage.png)

[GitHub Packages](https://github.com/features/packages) are a great way to host private npm modules. And with a few easy steps you can integrate it with Seed.

1. [Get your GitHub access token](https://help.github.com/en/packages/publishing-and-managing-packages/about-github-packages#about-tokens), make sure to give it the `read:packages` scope.

2. Add your access token as a secret

   [Store it as a secret]({% link _docs/storing-secrets.md %}) in Seed. For this example we'll name it, `GITHUB_ACCESS_TOKEN`.

3. Store your token in the build process and set the registry

   Add the following to your [build spec]({% link _docs/adding-a-build-spec.md %}) (`seed.yml`).

   ``` yml
    before_compile:
      - echo @OWNER:registry=https://npm.pkg.github.com >> ~/.npmrc
      - echo //npm.pkg.github.com/:_authToken=$GITHUB_ACCESS_TOKEN >> ~/.npmrc
   ```

   Where `OWNER` is your GitHub username or organization name.

A quick note on why we are setting the `~/.npmrc` instead of the `.npmrc`. Most folks use [serverless-webpack](https://github.com/serverless-heaven/serverless-webpack) or [serverless-bundle](https://github.com/AnomalyInnovations/serverless-bundle) to package their Lambda functions. As a part of the package step, serverless-webpack does an extra `npm install` (in a temp directory). Currently it does not use the `.npmrc` in your project root. And so we need to set it in our user space explicitly.

You can read more about [using private npm modules over on our docs]({% link _docs/private-npm-modules.md %}).

