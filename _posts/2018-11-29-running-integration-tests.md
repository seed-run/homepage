---
layout: post
title: Running Integration Tests
image: /assets/social-cards/post-deploy-phase.png
author: frank
---

As we continue to provide better support for [Serverless Framework](https://serverless.com) applications with multiple services, we are rolling out the ability to add a post-deploy phase to your deployment workflow.

![Post Deploy Phase](/assets/blog/running-integration-tests/post-deploy-phase.png)

To give a little context; Seed allows you to configure the CI/CD workflow for your mono-repo Serverless apps by letting you set up [Deploy Phases]({% link _docs/configuring-deploy-phases.md %}). It is very usually the case that you want to run integration tests or other post-deployment scripts after all your services are deployed. This is pretty easy to configure in Travis or Circle if you have a single service in your application. However, for applications with multiple services it can be tricky to configure and manage the workflow.

### Add a Post-Deploy Phase

Enter the concept of [Post-Deploy Phases]({% link _docs/adding-a-post-deploy-phase.md %}). You can now configure a post-deploy phase in your deployment workflow where you can add the tests (or any other scripts) that you'd like to run.

![Enable a Post-Deploy Phase](/assets/blog/running-integration-tests/enable-a-post-deploy-phase.png)

We give you the flexibility to configure a post-deploy phase on a per stage basis. This allows you to customize the type of scripts you want to run, in say dev vs prod.

Post-deploy phases are just another way Seed is making it ridiculously simple to manage deployments for your Serverless applications.

You can read further about [adding a post-deploy phase in our docs]({% link _docs/adding-a-post-deploy-phase.md %}).
