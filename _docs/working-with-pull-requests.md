---
layout: docs
title: Working with Pull Requests
---

When a pull request is opened, Seed receives a pull request notification from GitHub. Seed will then build, test, and deploy the pull request commits automatically into a new stage. The new pull request stage will receive a unique API Gateway endpoint just like any other stage. Seed will also build and deploy to the stage when commits are added to the pull request.

> We currently support pull requests only for GitHub.

[Contact us](mailto:{{ site.email }}) if you'd like to use it for Bitbucket or GitLab.

### Enable Auto-Deploy Pull Requests

By default, auto-deploying PRs are disabled. You can enable them by heading to your app and select the **Pipeline** tab.

![App Pipeline](/assets/docs/working-with-pull-requests/app-pipeline.png)

Select **Enable Auto-Deploy PRs**.

![Enable auto deploy pull requests](/assets/docs/working-with-pull-requests/enable-auto-deploy-pr.png)

Here you can specify a stage to copy the environment variables and other settings from. For example, your `dev` stage might be configured with environment variables for your app and with a set of IAM credentials specific for dev deployments. By selecting the `dev` stage, any stage that is automatically created for a new branch will copy the settings from the `dev` stage.

Seed will copy the following settings (if available) from the selected stage:

- IAM settings
- Post-deploy phase
- Notification settings
- Environment variables

You also have the option here to remove the PR stage and the deployed resources once the PR is closed.

![Auto-deploy pull request options](/assets/docs/working-with-pull-requests/auto-deploy-pr-options.png)

Next, let's work through the PR workflow.

### Create a PR

Create a pull request.

![Create Pull Request](/assets/docs/working-with-pull-requests/create-pull-request.png)

You'll notice that Seed will automatically start building the PR.

![Seed PR building check in GitHub](/assets/docs/working-with-pull-requests/seed-pr-building-check-in-github.png)

And in the Seed console you should see a new pull request stage created and building.

![Pull Request Stage Building](/assets/docs/working-with-pull-requests/pull-request-stage-building.png)

For monorepo Serverless apps, you can keep an eye on the progress as services get deployed.

![Seed PR building check in GitHub](/assets/docs/working-with-pull-requests/seed-pr-building-check-progress-in-github.png)

GitHub will let you know once the PR has been built.

![Seed PR building complete in GitHub](/assets/docs/working-with-pull-requests/seed-pr-building-complete-in-github.png)

Seed adds some useful info once your PR has been built.

![Seed PR complete info in GitHub](/assets/docs/working-with-pull-requests/seed-pr-complete-info-in-github.png)

In the above screenshot:

1. Seed will add a comment with a list of any deployed API endpoints. This is useful for cases where you have a frontend application that needs to be tested against this endpoint.

2. And the **View deployment** button in the environments section takes you to the deployed stage in Seed.

Also, if the PR fails to deploy, the **Details** link will take you straight to the build logs on Seed.

![Seed PR building failed in GitHub](/assets/docs/working-with-pull-requests/seed-pr-building-failed-in-github.png)

### Environment Variables

Seed also takes care of the environment variables and secrets for your pull requests. The variables defined in the `serverless.yml` for the _default_ stage (selected above in the settings) are made available to the pull request stage. [Secret variables]({% link _docs/storing-secrets.md %}) are also copied from the _default_ stage.

> Environment variables and secrets of the default stage are automatically available to the pull request build

In the example above, the _default_ stage, **dev** is connected to the **master** branch. This means that any pull requests stages will use environment variables set for the **dev** branch. And the secrets for the **dev** stage will also be available to the pull request build.

Say for example your `serverless.yml` looks like:

``` yaml
service: service-name

custom:
  myEnvironment:
    MESSAGE:
      production: "This is production environment"
      dev: "This is development environment"

provider:
  name: aws
  environment:
    MESSAGE: ${self:custom.myEnvironment.MESSAGE.${opt:stage}}
```

Any pull requests, will have the `process.env.MESSAGE` set to `This is development environment`.

Once the pull request is merged a build is automatically triggered in the upstream stage and an updated build with the merged code is created. Alternatively, you can directly promote a build from the pull request stage without merging the pull request. This is useful when you are deploying a hotfix.

You can now merge the pull request and optionally remove the PR branch by hitting **Delete branch** in GitHub.

![GitHub delete PR branch](/assets/docs/working-with-pull-requests/github-delete-pr-branch.png)

If you have the **Remove the stage and all the resources when the PR is closed** option enabled above, Seed will automatically remove the stage once the PR is closed.

![Seed auto-remove PR branch](/assets/docs/working-with-pull-requests/seed-auto-remove-pr-branch.png)

By enabling Auto-Deploy PRs, Seed makes it really easy to work with pull requests on GitHub.
