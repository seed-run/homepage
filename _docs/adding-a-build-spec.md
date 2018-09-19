---
layout: docs
title: Adding a Build Spec
---

While [Seed](/) does not need a build spec to configure your pipelines or your project, there are cases where you need to run some scripts during the build process.

### Seed.yml

To do this, just add a `seed.yml` in the root of your project directory. Here is the basic skeleton of our build spec.

``` yml
before_compile:
  - echo "Before compile"

before_build:
  - echo "Before build"

before_deploy:
  - echo "Before deploy"

after_deploy:
  - echo "After deploy"
```

The above commands are run in the following situations:

- `before_compile`

   Seed starts the build process by doing a `npm install` (for Node.js projects), `pip install -r requirements.txt` (for Python projects), or `make` (for Go projects). The `before_compile` step let's you run commands before this. This can be useful for [configuring private npm modules]({% link _docs/private-npm-modules.md %}). This step is not run when a build is promoted to production.

- `before_build`

   The actual build portion for Seed is the `serverless package` command that creates the build. The `before_build` step let's you run your commands before this happens. This step is not run when a build is promoted to production.

- `before_deploy`

   After the build packages are created, Seed deploys these using the `serverless deploy` command. The `before_deploy` let's you run your commands before this happens. This step is run for all builds and also when they are promoted to production. You can distinguish between the cases by using the `$SEED_STAGE` build environment variable.

- `after_deploy`

   Finally, after the deployment is complete you can use the `after_deploy` step to run any post deployment scripts you might have. Again, this step is run for all builds and also when they are promoted to production. You can distinguish between the cases by using the `$SEED_STAGE` build environment variable.

### Build Environment Variables

Seed also has a couple of build environment variables that you can use to customize your build process. These should not be confused with the [secret environment variables]({% link _docs/storing-secrets.md %}) that are defined in the console.

- `$SEED_STAGE`: This is the name of the stage that is being built. The stage names are exactly as shown in the console.

- Secrets: All your [secrets in the Seed console]({% link _docs/storing-secrets.md %}) are also made available during the build process. For example, a secret environment variable called **TEST_VAR** would be available as `$TEST_VAR` in the build process.

The above configuration options can let you customize your build process.
