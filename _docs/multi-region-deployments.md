---
layout: docs
title: Multi-Region Deployments
---

[Seed](/) makes it easy to deploy your Serverless app to multiple regions.

### Setting the region for a stage

To start off, let's configure our production stage to deploy to a specific region.

Head over to your prod stage. And hit **Settings**.

![Prod stage](/assets/docs/multi-region-deployments/prod-stage.png)

Here, you'll notice the deployed region setting.

![Stage region setting](/assets/docs/multi-region-deployments/stage-region-setting.png)

By default, Seed does not specify a region while deploying your app. This means that Serverless Framework will use the default region specified in your `serverless.yml`. But to configure multi-region deployments, let's specify a stage we want to deploy our app to.

![Select deployed region setting](/assets/docs/multi-region-deployments/select-deployed-region-setting.png)

Now you'll notice that this region is used while deploying your app.

![Region setting in build log](/assets/docs/multi-region-deployments/region-setting-in-build-log.png)

Note that, once a stage has been deployed, Seed will not allow you to change the region. This is because deploying to a new region is equivalent to deploying to a new stage. This orphans the previously deployed stage.

To deploy to another region, you'll need to create a new stage. 

### Add multiple prod stages

Head over to your app pipeline, and hit **Edit Pipeline**.

![App pipeline](/assets/docs/multi-region-deployments/app-pipeline.png)

Here you can add a new stage, and set it as a _production_ stage.

![Add new prod stage](/assets/docs/multi-region-deployments/add-new-prod-stage.png)

And just as above, you can head over to the stage settings, and select the region you want it deployed to.

### Promoting to prod

Now that you have multiple prod stages, you'll be able to promote them separately.

![Select prod stage for to promote](/assets/docs/multi-region-deployments/select-prod-stage-to-promote.png)

And that's it! Your app is now deployed to multiple regions.
