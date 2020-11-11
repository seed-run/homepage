---
layout: post
title: Second Generation build machines are in beta
categories: news
image: assets/social-cards/second-generation-build-machines.png
author: frank
tweet: 
---

The builds in Seed are about to get a lot faster. Today we are rolling out a new generation of build machines in beta. These Second Generation (SG) machines startup nearly 6x faster than our current ones.

![Second Generation build machine in build log](/assets/blog/second-generation-build-machines-are-in-beta/second-generation-build-machine-in-build-log.png)

### Background

Over the past few months, we've been hard at work at creating a completely new build infrastructure to drastically speed up your builds. A big part of this initiative is [the new build infrastructure that we are using to build CDK apps]({% link _posts/2020-09-23-fixing-cdk-deployments.md %}) on Seed.

We are now in the process of bringing those changes to your Serverless Framework projects. A big first step in that direction is a beta release of our new Second Generation build machines.

### Second Generation Build Machines

Typically, a build machine takes a little bit of time to provision the resources necessary to startup a new build. This can currently vary from 20s - 40s. While you are not charged for this provisioning time, it can slow down your builds. Especially, if you have [multiple deploy phases]({% link _docs/configuring-deploy-phases.md %}).

The new Second Generation machines reduce this down to 3s - 5s. Making a drastic difference in your overall build times.

During the beta, you can head over to your service settings and select the new Second Generation or _SG_ machines. You can [read more about this over on our docs]({% link _docs/build-machine-types.md %}#second-generation-machines).

![Select a Second Generation machine in the service settings](/assets/blog/second-generation-build-machines-are-in-beta/select-a-second-generation-machine-in-the-service-settings.png)

Note that, as we are scaling up capacity for these new machines, Seed might end up falling back to an equivalent First Generation machine for some builds.

The new Second Generation machines will also allow us to completely optimize the build process in the future. Our goal is to ensure that your Serverless apps are deployed as fast as possible on Seed!

So give the new machines a try and let us know what you think!
