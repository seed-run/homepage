---
layout: post
title: Simplifying Seed
author: jay
---

As we welcome 2019, I wanted to share the release of a major update to Seed and a little bit about our future direction.

![New Seed Homepage](/assets/blog/simplifying-seed/new-seed-homepage.png)

We've added a couple of features to make it easier to work with stages across services and we've re-organized the flows in the app. Before we go over the changes in this update, let me take a step back and talk about the problem we are trying to solve. It'll also give you a peek into how we do product development at Seed.

### The Problem

Back when Seed had first launched, it was a fully-managed CI/CD for [Serverless Framework](https://serverless.com) apps that had a single service. This meant that any action that you carried out on that service (promote, rollback, or a manual deployment) applied to the entire stage that you were working in. So for example, if you rolled back in your _production_ stage it was really just rolling back the service in that stage. And to do this action, you simply went into the _production_ stage and picked the build you wanted to rollback to.

However, as Seed grew to support multiple services within a Serverless app, this became a little complicated. It added an extra layer of organization. Now the action described above needed you to navigate to the _production_ stage, select the service you wanted to rollback, and then from the list of builds pick the one you wanted. This extra layer also made it hard to access the settings that were specific to a stage.

To illustrate this a bit, let's suppose our original page structure looked like so:

```
my-serverless-app
+-- stages
|   +-- production
|   +-- staging
|   +-- dev
|   +-- ...
|...
```

And the structure with multiple services would look something like:

```
my-serverless-app
+-- stages
|   +-- production
|       +-- service1
|       +-- service2
|       +-- service3
|   +-- staging
|       +-- service1
|       +-- service2
|       +-- service3
|   +-- alpha
|       +-- service1
|       +-- service2
|       +-- service3
|   +-- dev
|       +-- service1
|       +-- service2
|       +-- service3
|   +-- ...
|...
```


Now you might be wondering, how bad can an extra layer of organization really be? Turns out, it can be really confusing. This extra layer applied to not just the services pages and settings but also to the build pages themselves. It was also hard to direct our users to this "service in a certain stage" page. We even added a little UI component to try and make it clear that you were on this portion of the app, but to no avail.

![Service Stage Component](/assets/blog/simplifying-seed/service-stage-component.png)

You might know that we use Seed internally to deploy Seed, and not surprisingly our team would get tripped up by this issue as well! You would routinely get lost as you navigated the app. You would find a specific setting you were looking for after digging around. And only later be confused about how to get back to it. But before we could fix this we wanted to talk to our users about it and confirm our suspicions. 

### User Feedback

A big part of our product development process here at Seed involves talking to our users. Now we had casually spoke to a few of our users about this issue and they had politely mentioned the problem to us. But we decided to run a survey to get better insights into how our users were using the app.

Nearly a month ago we asked a subset of our users what they liked about Seed and what we could do to improve. And not surprisingly we heard back that they were confused about how the app was organized. They also had some suggestions on how to fix it. We loved running the survey because the combination of hearing about what people like about your product and what you can fix gives you a clear sense that you are talking to the right set of your users. This is especially true when your users are using your product to fulfill a broad set of needs.

### The Fix

The user feedback really added a charge to our team and we were motivated as ever to solve this. And the solution was remarkably simple. Instead of trying to find the best way to organize the existing set of pages, simply re-organize the main functions on those pages and eliminate the extra layer.

In essence, we moved certain settings over to the stage page and made it act on all the services in a stage. You might have seen some of our previous updates detailing these:

- [Redesigning the Homepage]({% link _posts/2018-11-15-redesigning-the-homepage.md %})
- [Stage Environment Variables]({% link _posts/2018-11-28-stage-environment-variables.md %})
- [Stage Notifications]({% link _posts/2018-12-11-stage-notifications.md %})

In this update we also made **promote**, **rollback**, and **manual deploy** act on all the services across a stage. Let's quickly look at these in a bit more detail.

#### Promote

You can now promote entire stages of your app. We are allowing you to do this right from the homepage of your app.

![Promote from Pipeline](/assets/blog/simplifying-seed/promote-from-pipeline.png)

Promoting all the services in a stage also, brings up the CloudFormation Change Set for all the services combined.

![Confirm CloudFormation Change Set](/assets/blog/simplifying-seed/confirm-cloudformation-change-set.png)

And we still let you promote individual services.

![Promote individual service](/assets/blog/simplifying-seed/promote-individual-service.png)

This ensures that you can still push a hotfix for a specific service forward to production if necessary. 

#### Rollback

Rollbacks also apply across all the services in a stage.

![Rollback a stage](/assets/blog/simplifying-seed/rollback-a-stage.png)

And you can now rollback in any stage, not just in production!

Finally, rollbacks are smart enough to recognize which services need to be rolled back to which version. So for example, if you've pushed an update to a specific service and you rollback to an older build, Seed will figure out the specific state of the services for the build you are rolling back to.

#### Manual Deploy

Just as the promote feature above, you can manually deploy an entire stage.

![Manual Deploy from pipeline](/assets/blog/simplifying-seed/manual-deploy-from-pipeline.png)

Or just deploy a single service in a stage.

![Manual Deploy single service](/assets/blog/simplifying-seed/manual-deploy-single-service.png)

### Re-organization

The changes above allow us to drastically reduce the complexity of the Seed console by removing an extra layer of complexity. So now we can go from:

```
my-serverless-app
+-- stages
|   +-- production
|       +-- service1
|       +-- service2
|       +-- service3
|   +-- staging
|       +-- service1
|       +-- service2
|       +-- service3
|   +-- alpha
|       +-- service1
|       +-- service2
|       +-- service3
|   +-- dev
|       +-- service1
|       +-- service2
|       +-- service3
|   +-- ...
|...
```

To this:


```
my-serverless-app
+-- stages
|   +-- services
|       +-- service1
|       +-- service2
|       +-- service3
|   +-- production
|   +-- staging
|   +-- alpha
|   +-- dev
|   +-- ...
|...
```

To add to this, we visually distinguish the various pages to make it clear which page you are on. Finally, we also redesigned the build pages.

![New Build page](/assets/blog/simplifying-seed/new-build-page.png)

Along with the build log pages.

![New Build log page](/assets/blog/simplifying-seed/new-build-log-page.png)

### Looking Ahead

We hope that this update makes it easier to manage deployments for your Serverless app. We'll be sure to reach out in a few weeks to see if you have any additional feedback on the new design and what we can do to improve.

The above process is a glimpse at how we do product development at Seed. We meld our product insights with concrete user feedback to create something that you'd love to use. Our goal is to make it effortless and convenient to deploy your Serverless Framework app to AWS. And we want to continue to improve this process.

As we look ahead to 2019, we are incredibly excited about what we have in our roadmap. We still think it is way too complicated to deploy and manage your Serverless applications and we have some really good ideas on improving it. Again, based not just on our product intuitions but the feedback we continually receive from the community and our users.

A big thanks to everybody that was kind enough to give us their feedback and for taking part in our journey. Here is to a great 2019! &#x1F942;
