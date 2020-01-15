---
layout: docs
title: Adding a Build Spec
---

While [Seed](/) does not need a build spec to configure your pipelines or your project, there are cases where you need to run some scripts during the build process. You can get a sense of the different build steps by looking at one of your build logs.

![Build logs screenshot](/assets/docs/adding-a-build-spec/build-logs-screenshot.png)

### Seed.yml

To hook into the build process, add a `seed.yml` in the root of your project directory. Here is the basic skeleton of our build spec.

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

Below is a brief description of when these commands are run.

- `before_compile`

   Seed starts the build process by doing a `npm install` (for Node.js projects), `pip install -r requirements.txt` (for Python projects), or `make` (for Go projects). The `before_compile` step let's you run commands before this. This can be useful for [configuring private npm modules]({% link _docs/private-npm-modules.md %}). This step is not run when a build is promoted to production.

- `before_build`

   The actual build portion for Seed is the `serverless package` command that creates the build. The `before_build` step let's you run your commands before this happens. This step is not run when a build is promoted to production.

- `before_deploy`

   After the build packages are created, Seed deploys these using the `serverless deploy` command. The `before_deploy` let's you run your commands before this happens. This step is run for all builds and also when they are promoted to production. You can distinguish between the cases by using the `$SEED_STAGE_NAME` build environment variable.

- `after_deploy`

   Finally, after the deployment is complete you can use the `after_deploy` step to run any post deployment scripts you might have. Again, this step is run for all builds and also when they are promoted to production. You can distinguish between the cases by using the `$SEED_STAGE_NAME` build environment variable.

### Build Environment Variables

Seed also has a couple of build environment variables that you can use to customize your build process. These should not be confused with the [secret environment variables]({% link _docs/storing-secrets.md %}) that are defined in the console.

- `$SEED_STAGE_NAME`: The name of the stage that is being built. The stage names are exactly as shown in the console.
- `$SEED_APP_NAME`: The app name.
- `$SEED_SERVICE_NAME`: The name of the service.
- `$SEED_BUILD_ID`: The build id.
- `$SEED_BRANCH`: The Git branch used in the build process. Does not apply to promotions and rollbacks. For PR stages, this is the branch the PR was submitted to.
- `$SEED_PULL_REQUEST_NUMBER`: For PR stages, this is the number of the Pull Request.

- Secrets: All your [secrets in the Seed console]({% link _docs/storing-secrets.md %}) are also made available during the build process. For example, a secret environment variable called **TEST_VAR** would be available as `$TEST_VAR` in the build process.

For example, let's take a build URL in the console:

```
https://console.seed.run/jayair/serverless-app/stages/dev/builds/32/services/users
```

Here the `$SEED_APP_NAME` would be `serverless-app`, `$SEED_STAGE_NAME` would be `dev`, `$SEED_SERVICE_NAME` would be `users`, and `$SEED_BUILD_ID` would be `32`.

### Custom Build Environment Variables

Environment variables that are set in the build spec do not persist across commands. This means that in the following build spec, `$MY_VAR` will not be printed out.

``` yml
before_compile:
  - export MY_VAR=hello
  - echo $MY_VAR
```

To ensure that your custom build environment variables persist across commands; Seed allows you to do something similar to [CircleCI](https://circleci.com/docs/2.0/env-vars/#using-bash_env-to-set-environment-variables). You export your custom environment variables to a `$BASH_ENV` and Seed will load that on every command.

So a variation of the above with `$BASH_ENV` looks like this:

``` yml
before_compile:
  - echo 'export MY_VAR=hello' >> $BASH_ENV
  - echo $MY_VAR
```

In this case `$MY_VAR` is loaded from `$BASH_ENV` and should be printed out correctly.

### Other Options

You can also add the following to your `seed.yml` to [deploy all your services without checking if anything has been updated]({% link _docs/deploying-monorepo-apps.md %}).

``` yml
check_code_change: false
```

### AWS CLI

The scripts in your build spec are run in an environment that are using your AWS IAM credentials. This means that you can directly use any AWS commands in your script using the AWS CLI without having to configure it.

---

### Build Spec Examples

Here are a couple of examples of what you could do in a build spec.

#### Run a script after deploy only in prod 

Let's assume your production stage is called `prod`.

```
after_deploy:
  - if [ $SEED_STAGE_NAME = "prod" ]; then echo 'deployed prod'; fi
```

#### Run a script after deploying a specific service

Let's assume your service is called `users`.

```
after_deploy:
  - if [ $SEED_SERVICE_NAME = "users" ]; then echo 'deployed users'; fi
```

#### Install PostgreSQL

If you need to start a PostgreSQL server locally for tests.

```
before_compile:
  - apt-get install wget ca-certificates -y
  - wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add -
  - sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ `lsb_release -cs`-pgdg main" >> /etc/apt/sources.list.d/pgdg.list'
  - apt-get update
  - apt-get install postgresql postgresql-contrib -y
```
