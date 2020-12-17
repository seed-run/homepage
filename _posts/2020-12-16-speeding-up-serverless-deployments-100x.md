---
layout: post
title: Speeding up Serverless deployments 100x
categories: news
image: assets/social-cards/100x-faster-deploys.png
author: frank
tweet: 
---

In this post we'll be looking at how Seed can speed up the deployment time of your Serverless app by 100x. It'll bring into focus all the improvements that we've rolled out over the past couple of months.

![Seed incremental lambda deploy build log](/assets/blog/speeding-up-serverless-deployments-100x/seed-incremental-lambda-deploy-build-log.png)

Serverless Framework apps, as you may know are made up of individual services. Each service is a CloudFormation stack that's deployed to AWS. Most real-world apps have:

- At least **20-40 services**
- Each service is usually made up of **12-20 Lambda functions**
- And a service can easily take **2-4 mins to deploy**

## Traditional CIs

Typically, most teams start off using a service like [Travis CI](https://travis-ci.com) or [CircleCI](https://circleci.com) to deploy their app. They'll use a simple build script that **loops through all the services** in the app and deploys them one after the other.

So the entire app takes **40-160 mins to deploy**.

Now you can optimize this a little by caching the `node_modules/` directories. But most traditional CIs simply download your cache from an S3 bucket and unzip them. The unzip portion is quite slow for directories with thousands of files, like the `node_modules/` directories. And you end up having to do an `npm install` any way. So this _"optimization"_ ends up making a very small difference.

## Concurrent Deploys

The real fix here is to deploy all your services concurrently. But you'll need to worry about a couple of things:

1. **Dependencies between services**
   
   Some services might need some other services to be deployed before it. So not everything can be deployed concurrently.

2. **Rate limiting errors**

   When you deploy a large number of services concurrently, you'll run up against various AWS rate limits. So you'll need to gracefully handle these failures and retry the deployment.

To handle these cases, you can imagine your build scripts will start to get a lot more complicated. It's common for folks to have build scripts that are 500-1000 lines long. At some point these scripts start to become unmaintainable.

Seed on the other hand deploys **all your services concurrently and reliably**. All without a build spec. And you can also configure [Deploy Phases]({% link _docs/configuring-deploy-phases.md %}) to specify the order in which your services need to be deployed.

![Seed deploy phases build details](/assets/blog/speeding-up-serverless-deployments-100x/seed-deploy-phases-build-details.png)

In the example above, we've got an app with 30 services deployed in 2 phases. The deployment time is now down to roughly **8 mins**.

So far, so good. Now let's get to the fun stuff.

## Incremental Service Deploys

The real fun begins when you make a change and have Seed deploy it.

![Seed incremental service deploy details](/assets/blog/speeding-up-serverless-deployments-100x/seed-incremental-service-deploy-details.png)

Here we are making a change to one of our services. And you'll notice that Seed automatically skips all the other services.

This is thanks to [Incremental Service Deploys]({% link _docs/incremental-service-deploys.md %}). Seed by default looks at the Git log to figure out if a change has been made in a specific service.

The custom infrastructure that we've built at Seed is optimized to the point that it doesn't even need to run a build job to skip a certain service. We use a **large number of concurrent background jobs** to check if a service needs to be deployed, while the build container for that service is being initialized!

Note that, our build machines are optimized to get started as fast as possible. Usually in around **3-5 secs**, thanks to our recently released [Second Generation Machines]({% link _posts/2020-11-10-second-generation-build-machines-are-in-beta.md %}).

## Caching Optimizations

Now let's step inside the build of a service that was updated.

![Seed cache optimization build log](/assets/blog/speeding-up-serverless-deployments-100x/seed-cache-optimization-build-log.png)

The app we are deploying has a `node_modules/` directory that's **1GB in size**. Seed does a couple of optimizations in the background to ensure that this is downloaded and unzipped as fast as possible. It also intelligently speeds up the actual `npm install` step.

Note that, this is supported for monorepo apps and [Yarn Workspaces](https://classic.yarnpkg.com/en/docs/workspaces/) as well.

## Incremental Lambda Deploys

Once the service has been packaged, Seed does a quick check to:

- Figure out if the CloudFormation or Serverless Framework config has been updated
- If not, then it looks at which of the Lambda functions have been updated

Once Seed figures out which Lambda functions need to be deployed, it'll call AWS directly and update them. And it does this concurrently. All without doing a CloudFormation update. The result is an **update that takes 0.65 secs**.

![Seed incremental lambda deploy build log](/assets/blog/speeding-up-serverless-deployments-100x/seed-incremental-lambda-deploy-build-log.png)

This is all thanks to what we call [Incremental Lambda Deploys]({% link _docs/incremental-lambda-deploys.md %}). And the [Serverless Seed plugin](https://github.com/seed-run/serverless-seed).

The entire deployment process took around **50 seconds**. That's deploying 30 separate Serverless services in under a minute! As opposed to the initial almost 90 minutes. **An improvement of 100x**!

## Bonus

Now if you're like us, you're probably asking yourself; _where was all that 50 secs spent?_ It turns out, that Seed has optimized every single step, aside from the `serverless package` command.

In our case we are using [Webpack](https://webpack.js.org) to individually package our Lambda functions. We are using the [serverless-bundle](https://github.com/AnomalyInnovations/serverless-bundle) plugin.

To speed this up, we can use [esbuild](https://esbuild.github.io) instead of Webpack. Using the [serverless-esbuild](https://github.com/floydspace/serverless-esbuild) plugin, you'll notice that it's about **10x faster** than Webpack. It's not as full featured as Webpack but depending on your app, you might be able to use it as is.

We can also kick things up a notch by using a [more powerful machine]({% link _docs/build-machine-types.md %}).

Now our incremental deploys should take only 15 seconds!

## Summary

The above optimizations are a culmination of efforts over the last couple of months. Seed's custom infrastructure can now deploy your Serverless apps 100x faster. Fixing one of the biggest issues of using Serverless at scale.

To quickly recap, Seed can now:

1. Deploy all your Serverless services concurrently and reliably
2. Incrementally deploy only the services that've been updated
3. Optimize how your dependencies are cached
4. Incrementally and concurrently deploy only the Lamda functions that've been updated
5. Use high performance build machines that start up almost instantly

And just as a reminder, Seed charges you based on the build minutes you use. So if your deployments are 100x faster, imagine how that'll impact your usage!

All these changes are available to all our Seed users, all across [our pricing plans]({% link pricing.html %}). We can't wait for you to try it!

If you are not currently using Seed and are figuring out how to; [feel free to get in touch with us](mailto:{{ site.email }}). Our team will be more than happy to get you started.
