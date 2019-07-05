---
layout: post
title: Monorepo Service Dependencies
image: /assets/social-cards/deploy-phases.png
categories: news
author: frank
---

Handling service dependencies has been a long standing problem for monorepo Serverless apps. Today we are introducing the concept of deployment phases to help address this issue.

![Configure Deploy Phases](/assets/blog/mono-repo-service-dependencies/configure-deploy-phases.png)

### Background

A little background before we look at how deploy phases work. If you've designed Serverless apps with multiple services or followed [our Serverless Stack guide on monorepo apps](https://serverless-stack.com/chapters/organizing-serverless-projects.html); you'll notice an obvious problem. Some services end up depending on some others. This could be your API service depending on the _infrastructure_ type services (setting up databases, queues, S3 buckets, etc). This means that the API service needs to be deployed after the infrastructure services. This can introduce a layer of complexity in your CI/CD pipelines that can make it hard to work with. You typically end up creating custom scripts to handle this, or worse deploy them manually.

### Our Motivations

This is a problem that we've encountered internally while deploying Seed itself! We also know quite a few folks personally that have been looking for find elegant solutions for this. So you can imagine our motivation for wanting to fix this. We wanted to make sure that we created a solution that was both easy to use and simple to visualize.

### Deploy Phases

And that is how we ended up with the idea for Deploy Phases. You might have noticed [our recent homepage redesign]({% link _posts/2018-11-15-redesigning-the-homepage.md %}). As a part of that redesign, we now show you all the different services that are a part of a given build.

![Deployment workflows](/assets/blog/mono-repo-service-dependencies/deployment-workflows.png)

The workflow portion of the build illustrates how the entire build was completed. In this case, all the services are deployed concurrently and the entire build is marked as completed when they are all done.

With Deploy Phases, you can add multiple phases to your deployment workflow. You can do this by hitting **Manage Deploy Phases** from your app settings. 

![Configure new Deploy Phases](/assets/blog/mono-repo-service-dependencies/configure-new-deploy-phases.png)

With multiple deploy phases, all the services in a phase need to complete before moving on to the next one. This gives you a simple and intuitive way of managing your service dependencies.

You can read more about [Configuring Deploy Phases in our docs]({% link _docs/configuring-deploy-phases.md %}).

Configuring deployment phases is just one way Seed is helping you manage your CI/CD pipelines for Serverless Framework applications on AWS.
