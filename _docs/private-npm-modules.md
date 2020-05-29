---
layout: docs
title: Private npm Modules
---

For Node.js projects you might be using private npm modules as dependencies.

### npm Registry

If you are using npm to host your private modules, do the following:

1. [Get your npm authentication token](https://docs.npmjs.com/private-modules/ci-server-config#getting-an-authentication-token)

   This is usually in a `~/.npmrc` file on your local machine. Follow [these steps](https://docs.npmjs.com/private-modules/ci-server-config#getting-an-authentication-token) to get your token.

2. Add your npm token as a secret

   Just like any other environment variable, follow [these steps]({% link _docs/storing-secrets.md %}) to add your token as a secret in the Seed console. For this example we will name your environment variable `NPM_TOKEN`.

3. Store your token in the build process

   Add the following to your [build spec]({% link _docs/adding-a-build-spec.md %}) (`seed.yml`).

   ``` yml
    before_compile:
      - echo //registry.npmjs.org/:_authToken=$NPM_TOKEN >> ~/.npmrc
   ```

   This uses the `NPM_TOKEN` environment variable from the previous step to create a `.npmrc` file to reference your private npm modules.

### GitHub Registry

If you are using GitHub to host your private modules, do the following:

1. [Get your GitHub access token](https://help.github.com/en/packages/publishing-and-managing-packages/about-github-packages#about-tokens), make sure to give it the `read:packages` scope.

2. Add your access token as a secret

   Follow [these steps]({% link _docs/storing-secrets.md %}) to add your token as a secret in the Seed console. For this example we will name your environment variable `GITHUB_ACCESS_TOKEN`.

3. Store your token in the build process and set the registry

   Add the following to your [build spec]({% link _docs/adding-a-build-spec.md %}) (`seed.yml`).

   ``` yml
    before_compile:
      - echo @OWNER:registry=https://npm.pkg.github.com >> ~/.npmrc
      - echo //npm.pkg.github.com/:_authToken=$GITHUB_ACCESS_TOKEN >> ~/.npmrc
   ```

   Replace `OWNER` with your GitHub username or organization name. This uses the `GITHUB_ACCESS_TOKEN` environment variable from the previous step to create a `.npmrc` file to reference your private npm modules.

#### Using ~/.npmrc instead of .npmrc 

Most folks use [serverless-webpack](https://github.com/serverless-heaven/serverless-webpack) or [serverless-bundle](https://github.com/AnomalyInnovations/serverless-bundle) to package their Lambda functions. As a part of the package step, serverless-webpack does an extra `npm install` (in a temp directory). As of writing this chapter, serverless-webpack does not use the `.npmrc` in your project root. And so we need to set it in our user space explicitly.


That's it! This should tell npm to properly reference your private modules.
