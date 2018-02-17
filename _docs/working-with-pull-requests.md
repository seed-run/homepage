---
layout: docs
title: Working with Pull Requests
---

When a pull request is opened, Seed receives a pull request notification from GitHub. Seed will then build, test, and deploy the pull request commits automatically into a new stage. The new pull request stage will receive a unique API Gateway endpoint just like any other stage. Seed will also build and deploy to the stage when commits are added to the pull request. We currently support pull requests only for GitHub. <a href="mailto:{{ site.email }}">Contact us</a> if you'd like to use it for Bitbucket or GitLab.

> Pull requests get their own unique endpoint and behave like any other stage

An important thing to note here is that the pull requests submitted to any branch that is not being tracked in Seed will not be built. This is because Seed uses the environment variables and secrets of the upstream stage to build the pull request.

> Pull requests submitted to branches that are not being tracked are ignored

Let's look at this in a bit more detail.

Create a feature branch.

``` bash
$ git checkout -b patch-1
$ git push -u origin patch-1
```

Create a pull request.

![Create Pull Request](/assets/docs/working-with-pull-requests/create-pull-request.png)

And in the Seed console you should see a new pull request stage created and building.

![Pull Request Stage Building](/assets/docs/working-with-pull-requests/pull-request-stage-building.png)

Once the stage is built and deployed, you can access its endpoint.

Seed also takes care of the environment variables and secrets for your pull requests. The variables defined in the `serverless.yml` for the upstream stage are made available to the pull request stage. [Secret variables]({% link _docs/storing-secrets.md %}) are also inherited from the upstream stage.

> Environment variables and secrets of the upstream stage are automatically available to the pull request build

In the example above, the pull request was submitted to the **master** branch, which is tracked by the **dev** stage. This means that any pull requests submitted to the **master** branch will use environment variables set for the **dev** branch. And the secrets for the **dev** stage will also be available to the pull request build.

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

Any pull requests submitted to **master** (or the stage **dev**), will have the `process.env.MESSAGE` set to `This is development environment`.

Once the pull request is merged a build is automatically triggered in the upstream stage and an updated build with the merged code is created. Alternatively, you can directly promote a build from the pull request stage without merging the pull request. This is useful when you are deploying a hotfix.

### Disable Auto-Deploy Pull Requests

Finally, you can disable auto-deploying pull requests by heading to the project settings and clicking on **Edit Project Info**.

![Project settings project info](/assets/docs/working-with-pull-requests/project-settings-project-info.png)

And deselecting the **Automatically deploy pull requests** checkbox and hitting **Save**.

![Deselect auto deploy pull requests](/assets/docs/working-with-pull-requests/deselect-auto-deploy-pull-requests.png)

This is useful if you are using tools that automatically generate pull requests.
