---
layout: post
title: Build Issues on April 8th, 2019
author: jay
---

On April 8th, 2019 from around 8:35 - 10:05 AM PDT, quite a few users on Seed experienced build issues. We want to share some details about what happened and what we are going to be doing about it moving forward.

To start with I'd like to apologize to our affected users for any disruption we might have caused.

### What happened

A majority of our internal processes rely on a plethora of AWS services. Between 8:35 AM and 10:05 AM PDT on April 8th, 2019 AWS experienced some downtime in the us-east-1 region. A large number of our processes are tied to this region and our inability to switch to a different region meant that the builds for a large number of our users abruptly failed. All the builds during this period were failing and the build logs were also inaccessible in many cases.

We worked to investigate the issues and communicated that directly to a number of our users. We also made sure to send out regular updates through [Twitter (@SEED_run)]({{ site.twitter }}). At around 10:05 AM PDT most of the processes were back operating normally.

### What are we doing to resolve the issues

We need to be able to shift workloads dynamically across regions to mitigate regional incidents like the one we faced on April 8th. Over the next couple of weeks we are going to be working on adding the ability to re-distribute workloads across regions.

We are also going to be working on being able to detect these issues as they happen and pass along this information in a more timely manner.


Once again, I'd like to apologize for any disruptions we might have caused. We know that deployments are a mission critical part of your team's workflow. And thanks to the affected users who were both patient and supportive as we worked through the incident.
