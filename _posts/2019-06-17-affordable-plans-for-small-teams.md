---
layout: post
title: Affordable Plans for Small Teams
image: /assets/social-cards/affordable-plans.png
categories: news
author: jay
---

We are happy to announce a couple of big changes to our pricing plans. Seed is now all the more affordable for startups and small teams.

Here are the main changes:

1. Our plans now start at $30/month, as opposed to $95/month.
2. The limit on our plans is changing from the number of builds to the build minutes used.

We are also increasing the usage limits on our plans while lowering the price per user. Here is a quick comparison of the our old and new paid plans:

|                           | Old | New               |
|---------------------------|---------------|--------------------|
| Price (per user/mo)       | $19           | $10                |
| Starting at (per mo)      | $95           | $30                |
| Usage limit (per user/mo) | 300 builds    | 1500 build minutes |
|---------------------------|---------------|--------------------|

You can read about the details in our [new pricing page]({% link pricing.html %}). If you are currently a Seed user, you can jump to the section at the bottom of this post to see how these changes will impact your account.


### Making Seed More Affordable

We've come to learn over the past few months that Seed is a perfect fit for small teams and startups. They really want to focus on developing their Serverless apps and not worry about the DevOps. However, our old paid plans started at $95/month. This happened to be outside the range for many small teams that are just getting started.

Our new [Team plan]({% link pricing.html %}), is priced at $10 a user/month and starts at $30/month. A perfect for small teams to get started with and it also works well as a team starts to grow. 


### Transparent Usage Limits

Previously, our plans were limited by the number of builds you were allowed to make. This was always a bit confusing. _What if some services deployed quicker than others? Would they count towards the limit all the same?_ You also might have read about our recent update of [only deploying services that have been changed]({% link _posts/2019-05-21-a-big-spring-update.md %}#only-deploy-updated-services). _Does that mean skipped builds do not count towards the limit?_

To clear up all of this confusion, we are switching the usage limits on our plans to build minutes. Here is a quick comparison of our free and paid plans in terms of number of builds vs build minutes.

|                 | Old | New |
|-----------------|--------------|---------------|
| Individual      | 200 builds          | 500 build minutes           |
| Team (per user) | 300 builds         | 1500 build minutes          |
|-----------------|--------------|---------------|

Under the new change, Seed will count the actual number of minutes it takes to deploy a service. Meaning that making a small change that deploys in a minute does not affect your limit as much as a large update that is making a ton of infrastructure changes.

![Build report panel with build times](/assets/blog/affordable-plans-for-small-teams/build-report-panel-with-build-times.png)

You can get a sense of the number of build minutes a deployment took by looking at your build page.

A quick note of how we compare to traditional CI services in terms of pricing. Most CI services charge you extra for building your services concurrently (and are very expensive). This is a bad fit for most Serverless apps that have multiple services. It means that your builds will either be very slow or very expensive. Seed on the other hand, has no limits on concurrency; your builds will deploy concurrently by default.

### How Do These Changes Affect Me?

We've got some great news if you are using our paid plans. While previously, you were limited to 5 users and 5 x 300 builds. We are increasing them to 10 users and 10 x 1500 build minutes, while keeping your monthly rate the same. Here is a quick comparison of the changes to your account.

|                 | Old | New |
|-----------------|--------------|---------------|
| Price (per mo) | $95          | $95          |
| # of users | 5          | 10         |
| Usage limit (per user/mo) | 1500 builds          | 15000 build minutes         |
| Add a user (per mo) | $19          | $10         |
|-----------------|--------------|---------------|

Of course, you are free to add or remove users from your account to match your needs.

### Looking Ahead

We are incredibly excited to make Seed more accessible to folks that are building their future on Serverless and AWS. And with this change, we'll be there with you every step of the way!
