---
layout: post
title: Redesigning the Homepage
image: /assets/social-cards/redesigning-the-homepage.jpg
categories: news
author: frank
---

Today we are introducing a redesigned homepage for Seed. The new homepage gives you a bird's-eye view of the state of your app and quick access to all the recent builds.

![Redesigned homepage](/assets/blog/redesigning-the-homepage/redesigned-homepage.png)

### The Story so Far

When we had first launched Seed, we only supported Serverless applications that had a single service. This meant that the current state of the application (the version of the build in the different stages) was the same as the state of the one service in the application. Hence, your homepage for the application just displayed the various stages and the current active build in that stage. It also meant that the only builds taking place in the entire application were taking place in that service. So if you needed to view this, you simply navigated to the specific stage and you could see a list of all the builds.

Over the last few months we have been gradually adding support for Serverless applications that have multiple services. This has increased the complexity of the Seed console. Specifically, it has added an extra layer of organization. Since each application is made up of multiple services, if you navigate to a stage you'll be presented with a list of all the services. And each service in that list would display the current active build in it. This made it hard to get a quick overview of the builds that were taking place in the app. You needed to drill down to each service in a specific stage to see the list.

### The New Homepage

With the redesign that we are introducing today; you get a very quick overview of the current state of the app and a quick list of the most recent builds.

![Redesigned homepage sections](/assets/blog/redesigning-the-homepage/redesigned-homepage-sections.png)

We can break down the new homepage into two sections:

1. The current state: A table that shows you the current build in all your services across all the stages
2. The history : A list of all the recent builds in the application

Upon navigating to a build, you can now see all the services that were a part of it.

![New build page](/assets/blog/redesigning-the-homepage/new-build-page.png)

In the above example, you'll notice that this build involved the deployment of three services that were carried out concurrently. These workflows are fairly simple but we will soon be allowing you to define them to support dependencies across services.

The pattern of the showing you the current state in conjunction with the build history is applied to a few of our other pages as well. Including the page that displays the stage.

![New stage page](/assets/blog/redesigning-the-homepage/new-stage-page.png)

And the service.

![New service page](/assets/blog/redesigning-the-homepage/new-service-page.png)

Of course, in both of the cases above you only see the list of the builds that are specific to the stage and service that you are viewing.

This means that if you happen to be only interested in what is happening in production, you can simply navigate to that. And you'll get a view of the current state of the services in production and the recent builds in it.

### Looking Ahead

We have a few more minor organizational changes on the way but we think this is a major step in helping you manage and monitor deployments for multi-service Serverless applications. We hope that these new changes simplify the CI/CD workflow for your Serverless Framework application. And we'd love to hear from you if you have any questions or comments!
