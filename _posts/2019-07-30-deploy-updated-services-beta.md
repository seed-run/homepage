---
layout: post
title: Deploying only the updated services is in beta
image: assets/social-cards/monorepo-deployments.png
categories: news
author: jay
---

One of our most popular feature requests is finally in beta today! Seed will now only deploy the services that have been updated in your monorepo Serverless app. To participate in the beta, [send us an email](mailto:{{ site.email }}) or contact us via the chat.

A little bit of a background before we dive into the details. Seed does a great job of managing [all the services in your Serverless app]({% link _docs/mono-repo-apps-in-seed.md %}). We also allow you to configure [Deploy Phases]({% link _docs/configuring-deploy-phases.md %}) to manage service dependencies. This means that you can easily spin up new environments completely automatically without ever touching a build script. And it works great even if you have a couple dozen services. 

However, there might be times when you just need to update a single service. In these cases deploying all your services makes the entire process slower. To tackle this problem, Seed relies on [Serverless Framework](https://serverless.com) to check if a service has been updated before deploying it. This check works great but it still needs to complete most of the build process along the way. This includes installing packages for your build. So while this is an optimization, it's not a great one. Additionally, this check isn't bulletproof and can be a bit buggy.

To fix this issue, we are releasing a new feature in beta today. Seed will check your commit history to see if any of the files (with respect to the current service) has been changed. If there are no changes, Seed will skip the entire build process. This means that your deployments will now be drastically faster and far more cost-effective.

The algorithm that Seed will use to see if the service has been updated, is fairly straightforward but it's worth taking a look. We have added a detailed chapter on this over on our docs; [Deploying Monorepo Apps]({% link _docs/deploying-monorepo-apps.md %}).

If you would like to participate in the beta, [send us an email](mailto:{{ site.email }}) or contact us via the chat.
