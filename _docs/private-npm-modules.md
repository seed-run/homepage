---
layout: docs
title: Private npm Modules
---

For Node.js projects you might be using private npm modules as dependencies. You can follow the steps below to ensure they are made available during the build process.

1. [Get your npm authentication token](https://docs.npmjs.com/private-modules/ci-server-config#getting-an-authentication-token)

   This is usually in a `~/.npmrc` file on your local machine. Follow [these steps](https://docs.npmjs.com/private-modules/ci-server-config#getting-an-authentication-token) to get your token.

2. Add your npm token as a secret

   Just like any other environment variable, follow [these steps]({% link _docs/storing-secrets.md %}) to add your token as a secret in the Seed console. For this example we will name your environment variable `NPM_TOKEN`.

3. Store your token in the build process

   Add the following to your [build spec]({% link _docs/adding-a-build-spec.md %}) (`seed.yml`).

   ``` yml
    before_compile:
      - echo "//registry.npmjs.org/:_authToken=$NPM_TOKEN" >> ~/.npmrc
   ```

   This uses the `NPM_TOKEN` environment variable from the previous step to create a `.npmrc` file to reference your private npm modules.


That's it! This should tell npm to use your token to reference your private modules.
