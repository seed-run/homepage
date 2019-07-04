---
layout: docs
title: Monorepo Apps in Seed
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

### Monorepo

A common way to organize your multiple services is to create a `services/` directory in your application and adding the various services there.

``` bash
$ ls services/
groups    posts     users
```

Here each service has it's own `serverless.yml`. Meaning you would deploy them by running the `serverless deploy` command inside each service directory. In effect, you have multiple projects in the same repository. This type of organization (multiple services in the same repo) is generally referred to as monorepo.

An alternative strategy is to completely separate the services into their own repositories. This is desirable when you are thinking of having different developers (or teams) manage those services on their own.

### Deployments

Monorepo apps can add a layer of complexity to your deployment process. Deploying your application involves co-ordinating deployment across multiple services.

> Seed by default deploys all the services in a monorepo app concurrently.

Seed simplifies this by deploying the entire application as a whole.

1. Start by [adding all the services in your application]({% link _docs/adding-a-service.md %}). The pipeline view of your app gives you a clear overview of the services and the specific builds that are deployed to it.

   ![App Pipeline view](/assets/docs/mono-repo-apps-in-seed/app-pipeline-view.png)

2. By default, all the services are deployed concurrently. You can configure the deployment order by hitting **Manage Deploy Phases** in the app settings. You can [read more about configuring deployment phases]({% link _docs/configuring-deploy-phases.md %}) here.

   ![configure deploy phases](/assets/docs/mono-repo-apps-in-seed/configure-deploy-phases.png)

3. A deployment to the app will now trigger all the services in the app to be deployed. Seed deploys all the services in a monorepo app concurrently.

   ![App deployment in progress](/assets/docs/mono-repo-apps-in-seed/app-deployment-in-progress.png)

4. Once you are ready to promote to production, you can pick the service and manually promote it.

   ![Promote service build](/assets/docs/mono-repo-apps-in-seed/promote-service-build.png)

### Environments

Seed also gives you a way to manage the environments across all the services in your app. This is especially useful when you have a large number of services.

The pipeline view of your app is a table where the columns are the various stages in your app. And the rows are the different services.

![App Pipeline view](/assets/docs/mono-repo-apps-in-seed/app-pipeline-view.png)

To get a better sense of this pipeline view let's click around a bit.

1. Clicking on a service row (dropdown) for example, gives you the ability to deploy or promote just that service.

   ![Service Stage](/assets/docs/mono-repo-apps-in-seed/service-dropdown.png)

2. Whereas, clicking on a stage (column header) shows you the various services deployed to that stage. It also shows you the builds that are deployed and the resulting deployment.

   ![App Stage](/assets/docs/mono-repo-apps-in-seed/app-stage.png)

Finally, the app's stage allows you to control the settings for all the services in the stage.

![App Stage settings](/assets/docs/mono-repo-apps-in-seed/app-stage-settings.png)

In the above example, using a set of custom IAM credentials would mean that all the services deployed to this stage will use this setting.

The stages and services in an app allow you to easily control your monorepo serverless apps in Seed.
