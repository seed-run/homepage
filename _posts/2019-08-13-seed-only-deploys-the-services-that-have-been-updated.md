---
layout: post
title: Seed only deploys the services that have been updated
image: assets/social-cards/monorepo-deployments.png
categories: news
author: jay
---

Starting today, [Seed](/) will only deploy the services that have been updated in your monorepo [Serverless app](https://serverless.com)!

This highly requested feature has been [in beta for the past two weeks]({% link _posts/2019-07-30-deploy-updated-services-beta.md %}). The feedback we've received has been great. It's been speeding up builds and is allowing people to add more services to their apps. 

### How it works

A little bit of a background before we look at how this feature works. Seed does a great job of managing [all the services in your Serverless app]({% link _docs/mono-repo-apps-in-seed.md %}). We also allow you to configure [Deploy Phases]({% link _docs/configuring-deploy-phases.md %}) to manage service dependencies. This means that you can easily spin up new environments completely automatically without ever touching a build script. And it works great even if you have a couple dozen services. 

However, there might be times when you just need to update a single service. In these cases deploying all your services makes the entire process slower. To tackle this problem, Seed relies on [Serverless Framework](https://serverless.com) to check if a service has been updated before deploying it. This check works great but it still needs to complete most of the build process along the way. This includes installing packages for your build. So while this is an optimization, it's not a great one. Additionally, this check isn't bulletproof and can be a bit buggy.

To fix this issue, Seed will check your commit history to see if any of the files (with respect to the current service) has been changed. If there are no changes, Seed will skip the entire build process for that service. This means that your deployments will now be drastically faster (and far more cost-effective).

The algorithm that Seed will use to see if the service has been updated, is fairly straightforward but it's worth taking a look. We have added a detailed chapter on this over on our docs; [Deploying Monorepo Apps]({% link _docs/incremental-service-deploys.md %}).

### Rollout Plan

Today we'll be rolling this out to all of our users on Seed. Here is what the rollout plan looks like:

1. It'll be turned on by default for **all new apps** on Seed.
2. For all your existing apps, we'll be turning it on for **all non-production environments** (or stages).
3. And **a week from now**, we'll turn it on for your **production environments** as well.

This'll give you a chance to get used to how the new deployment process works and fix any issues before it affects your production deployments.

### Opting out

We also have a way for you to opt out, in case you have a setup that is incompatible with this feature. You can simply add the following to your `seed.yml` and Seed will always deploy all your services.

``` yml
check_code_change: false
```

You can [read more about this in our docs]({% link _docs/adding-a-build-spec.md %}#other-options). And as always, you can [contact us](mailto:{{ site.email }}) if you have any questions.

With this update, Seed now perfectly supports Serverless Framework applications with multiple services. And your deployments will always be fast and efficient, even if you have dozens of services. A huge thanks to our beta testers for their feedback. And we continue to be excited as we work to make Seed the best way to deploy your Serverless apps on AWS!
