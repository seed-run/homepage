---
layout: docs
title: Mono-Repo Apps in Seed
---

[Serverless Framework](https://serverless.com) applications are made up of multiple services. A service can be thought of as a project that is based on a single `serverless.yml` file. By default, Serverless Framework applications start with a `serverless.yml` in the project root.

``` bash
$ ls
function.js     serverless.yml
```

Once your application grows you might find yourself wanting to organize it by splitting your single service into multiple services. Or you might run into a deployment error (like the one below) that forces you to split them up.

```
Error --------------------------------------------------

The CloudFormation template is invalid: Template format error: Number of resources, 201, is greater than maximum allowed, 200
```

### Mono-Repo

A common way to organize your multiple services is to create a `services/` directory in your application and adding the various services there.

``` bash
$ ls services/
groups    posts     users
```

Here each service has it's own `serverless.yml`. Meaning you would deploy them by running the `serverless deploy` command inside each service directory. In effect, you have multiple projects in the same repository. This type of organization (multiple services in the same repo) is generally referred to as mono-repo.

An alternative strategy is to completely separate the services into their own repositories. This is desirable when you are thinking of having different developers (or teams) manage those services on their own.

### Deployments

Mono-repo apps can add a layer of complexity to your deployment process. Deploying your application involves co-ordinating deployment across multiple services.

> Seed deploys all the services in a mono-repo app concurrently.

Seed simplifies this by deploying the entire application as a whole.

1. Start by [adding all the services in your application]({% link _docs/adding-a-service.md %}). The pipeline view of your app gives you a clear overview of the services and the specific builds that are deployed to it.

   ![App Pipeline view](/assets/docs/mono-repo-apps-in-seed/app-pipeline-view.png)

2. A deployment to the app will now trigger all the services in the app to be deployed. Seed deploys all the services in a mono-repo app concurrently.

   ![App deployment in progress](/assets/docs/mono-repo-apps-in-seed/app-deployment-in-progress.png)

3. Once you are ready to promote to production, you can pick the service and manually promote it.

   ![Promote service build](/assets/docs/mono-repo-apps-in-seed/promote-service-build.png)

### Environments

Seed also gives you a way to manage the environments across all the services in your app. This is especially useful when you have a large number of services.

The pipeline view of your app is a table where the columns are the various stages in your app. And the rows are the different services.

![App Pipeline view](/assets/docs/mono-repo-apps-in-seed/app-pipeline-view.png)

To get a better sense of this pipeline view let's click around a bit.

1. Clicking on a service (row header) for example, gives you a view of the stages (or environments) that apply to the service. It also shows you the past few builds for the respective stages.

   ![Service Stage](/assets/docs/mono-repo-apps-in-seed/service-stage.png)

2. Whereas, clicking on a stage (column header) shows you the various services deployed to that stage. It also shows you the builds that are deployed and the resulting deployment.

   ![App Stage](/assets/docs/mono-repo-apps-in-seed/app-stage.png)

Finally, the app's stage allows you to control the settings for all the services in the stage.

![App Stage settings](/assets/docs/mono-repo-apps-in-seed/app-stage-settings.png)

In the above example, using a set of custom IAM credentials would mean that all the services deployed to this stage will use this setting.

To drill down further, you click through to a service's specific stage setting.

![Service Stage settings](/assets/docs/mono-repo-apps-in-seed/service-stage-settings.png)

In this case, if you set the environment variables; it sets them for the specific stage of this service. And not for all the other services in the stage.

To help you distinguish between the various stages of a service, Seed will highlight this as `$Service-Name > $Stage-Name`.

![Service Stage combo identifier](/assets/docs/mono-repo-apps-in-seed/service-stage-combo-identifier.png)

The stages and services in an app allow you to easily control your mono-repo serverless apps in Seed.
