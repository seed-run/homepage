---
layout: docs
title: Incremental Service Deploys
redirect_from: /docs/deploying-monorepo-apps.html
---

A monorepo Serverless app is one where multiple Serverless services are in the same repo. This means that a commit will trigger a deployment to all the services in [Seed](/). However, this can be a slow process if you are only trying to deploy a change to a single service.

To fix this, Seed uses Incremental Service Deploys. It'll check to see if a service has been updated, before deploying it. This greatly speeds up your builds and also makes deployments cost-effective.

There are three algorithms Seed uses to check if a service has been updated:

1. Check the Git log for updates (Default)

   Seed looks at the Git log to see if any files related to the service have been updated. This is done by default for all services deployed through Seed.

2. Use Lerna to check updated packages

   Alternatively, if your project uses [Lerna](https://lerna.js.org) + [Yarn Workspaces](https://classic.yarnpkg.com/en/docs/workspaces/), then Seed can use the Lerna CLI to see a service has been updated. To use this algorithm, you'll need to add `check_code_change: lerna` to your [build spec]({% link _docs/adding-a-build-spec.md %}) — `seed.yml`.

3. Use pnpm to check updated packages

   Similar to Lerna, if your project uses [pnpm Workspaces](https://pnpm.io/workspaces), then Seed can use the pnpm CLI to see a service has been updated. To use this algorithm, you'll need to add `check_code_change: pnpm` to your [build spec]({% link _docs/adding-a-build-spec.md %}) — `seed.yml`.

Let's look at these in detail.

### Check the Git log for updates

By default, Seed uses a simple algorithm to determine if a service in your app needs to be deployed. The algorithm is based on the directory structure of your Serverless app. Let's look at the cases in detail.

1. Single service per repo

   Your app only has one service. In this case Seed will always run the deployment process for your service. It won't look at the Git log to check if it needs to deploy your app.

2. Services are organized in a flat directory structure

   Your app has multiple services and they are all in a directory on the same level. So it might look something like this:

   ```
   /
    libs/
    services/
      posts/
        serverless.yml
        handler.js
      groups/
        serverless.yml
        handler.js
      users/
        serverless.yml
        handler.js
   ```

   The algorithm used for this is fairly straight forward. To determine if Seed should deploy a service:

   - Check if a file in the current service directory has been changed. For example, a change to `/services/posts/handler.js` or `/services/posts/utils/format.js` would trigger a deployment in the **posts** service.
   - If a file has been changed outside the service's directory AND does not belong to any other services. For example, a change to `/libs/date-lib.js` would trigger a deployment in the **posts** service (and all the other services as well). While a change in `/services/users/handler.js` will not trigger a deployment in the **posts** or **groups** service. Note that, Seed only checks against services that have been added in the dashboard. So if you haven't added the **users** service in Seed, a change to `/services/users/handler.js` will trigger a deployment in all the other services.

   <br />Here is the algorithm in flowchart form to check if a service should be deployed.

   ![Flat directory services deployment algorithm](/assets/docs/deploying-monorepo-apps/flat-directory-services-deployment-algorithm.png)

   To summarize, if something changes in your service's directory it'll get deployed. And if something changes outside your service's directory but doesn't belong to any other services, then it'll get deployed as well.

3. Services are organized in a nested directory structure

   Your app has multiple services but they are nested inside each other. There are two variants of this. The first is where you have a service in your project root.

   ```
   /
    serverless.yml
    handler.js
    libs/
    services/
      posts/
        serverless.yml
        handler.js
      groups/
        serverless.yml
        handler.js
      users/
        serverless.yml
        handler.js
   ```
   
   The second is where you simply have a service inside another service's directory.

   ```
   /
    libs/
    services/
      posts/
        serverless.yml
        handler.js
        featured /
          serverless.yml
          handler.js
   ```

   In general, we advise against using these nested structures. It makes things more complicated than they need to be and are harder to maintain in the long run.

   The algorithm we use for this, adds an extra case on top of the one we looked at above. If a file has changed in another service's directory, but the directory is a parent of the current service, then we deploy the current service. Let's look at the nested structure above, where the **featured** service is nested inside the **posts** service. If the `/services/posts/handler.js` changes, then we will deploy the **featured** service as well. This is because the **posts** service is in a parent directory of the **featured** service. Note that, it doesn't need to be a direct parent. It just needs to contain the service in question.

   Here is the algorithm for the nested case in flowchart form.

   ![Nested services deployment algorithm](/assets/docs/deploying-monorepo-apps/nested-services-deployment-algorithm.png)

   So to summarize, it's the same as the one above, with the added caveat that Seed will deploy a service if the files changed belong to a service in a parent directory.

Seed will apply the above algorithm for each service in your app to decide if it needs to trigger a deployment process. A service with a skipped deployment step will look something like this:

![Skipped service with no code changes](/assets/docs/deploying-monorepo-apps/skipped-service-with-no-code-changes.png)

Finally, Seed will skip the above check and deploy all your services if:

- This is the first deployment
- The previous deployment had failed
- It's a [manual deploy with the force option enabled]({% link _docs/manually-deploying.md %}#force-deploys)
- The `check_code_change` is set to `false` [in your seed.yml]({% link _docs/adding-a-build-spec.md %}#other-options)

If you are trying to figure out why Seed deployed your service, you can check the details in your build log. Note the, `Checking for changes` section below.

![Seed found code changes in service](/assets/docs/deploying-monorepo-apps/seed-found-code-changes-in-service.png)

### Use Lerna to check updated packages

If you are using [Lerna + Yarn Workspaces to manage your monorepo Serverless project](https://serverless-stack.com/chapters/using-lerna-and-yarn-workspaces-with-serverless.html), Seed can use the Lerna CLI to figure out which of your services need to be deployed. To use this algorithm, add the following to your `seed.yml` in your project root.

``` yml
check_code_change: lerna
```

![Lerna check in Seed build log](/assets/docs/deploying-monorepo-apps/lerna-check-in-seed-build-log.png)

Let's look at how this algorithm works.

To begin with:

- If the app only has one service, then we simply deploy it.
- If the previous deployment had failed, then we skip the check and deploy it.
- If we are [manually deploying with the force option]({% link _docs/manually-deploying.md %}#force-deploys), then we skip the check and deploy it.

Note that, the above conditions apply to the Git log check algorithm as well.

Next:

1. Seed will run the `lerna ls --since ${prevCommitSHA} -all` to list all packages that have been changed since the last successful deploy. If the current service is in the list, we deploy it.
2. If there are other file changes in the Git log that don't belong to any packages in your Yarn Workspaces, then we deploy the current service.
3. If the two above conditions are not met, then we skip deploying this service.

If you are looking to get started with using Lerna + Yarn Workspaces for your Serverless app, we have a starter project for you — [**Serverless Lerna + Yarn Workspaces Monorepo Starter**](https://github.com/AnomalyInnovations/serverless-lerna-yarn-starter)

### Use pnpm to check updated packages

If you are using [pnpm Workspaces](https://pnpm.io/workspaces) to manage your monorepo Serverless project, Seed can use the pnpm CLI to figure out which of your services need to be deployed. The way it works is very similar to the Lerna algorithm. To use this algorithm, add the following to your `seed.yml` in your project root.

``` yml
check_code_change: pnpm
```

-------

The above checks makes it so that Seed will only deploy your services if the relevant parts of your code have been updated. This ensures that the deployments for your monorepo Serverless apps on Seed are fast and cost-effective.
