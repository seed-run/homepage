---
layout: docs
title: Deploying Monorepo Apps
---

A monorepo Serverless app is one where multiple Serverless services are in the same repo. This means that a commit will trigger a deployment to all the services in [Seed](/). However, this can be a slow process if you are only trying to deploy a change to a single service. There are two things that Seed does to fix this:

1. Check the Git log to see if the code for a service has been updated.
2. Rely on [Serverless Framework](https://serverless.com) to check if the Lambda package (code and CloudFormation template) has been changed.

This two step process works in tandem to only deploy the services that have been updated. This greatly speeds up your builds and also makes deployments cost-effective.

Let's look at these two checks in detail.

### 1. Check the Git log for updates

Seed uses a simple algorithm to determine if a service in your app needs to be deployed. The algorithm is based on the directory structure of your Serverless app. Let's look at the cases in detail.

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
- It's a manual deploy with the force option enabled

Once the process has been triggered, there is a further check that Seed (or Serverless Framework) will do to see if the deployment to AWS needs to be completed. Let's look at that next.

### 2. Check if the Lambda package has changed

Serverless Framework generates a package that it'll send to AWS when you run `serverless deploy`. Recall that Seed runs this command on your behalf. The newly generated package is compared to the most recent deployment package (as stored in S3). If there are no changes, then Serverless Framework will skip updating the service.

These two checks make sure that Seed will only deploy your changes if the relevant services have been updated. This ensures that the deployments for your monorepo Serverless apps on Seed are fast and cost-effective.
