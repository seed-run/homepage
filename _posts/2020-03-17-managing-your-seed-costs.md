---
layout: post
title: Managing your Seed costs
categories: news
author: jay
---

The next few months are going to be a difficult time for startups and businesses as we enter into a global economic slowdown. We'll all be looking for ways to cut costs and expenses in an effort to cope with this new reality.

As a startup, we know what most of our users will be going through over the next little while. Personally, I've had to do this before. Where you repeatedly go through all your expenses to figure out ways to save money. It's not fun.

I want to do what little we can to help you with that. We've always had [a very generous free tier and very competitive prices around build minutes]({% link pricing.html %}). However, we'll be rolling out a couple of changes to our pricing plans over the next month to further help you save. More on this below.

That said, there are a few things you can do to manage your Seed monthly usage. Below are a list of changes you can make to your workflow to cut down your costs. Starting with the ones that require the least amount of changes to the way you work.

Note that, some of these are specifically meant to reduce your build minutes usage and isn't necessarily what we think are the best practices. It would make sense to adopt some of them only while you are aggressively cutting costs.

### Reducing build minutes usage

Before we start, check out your monthly build minutes usage by heading over to your organization's billing settings on Seed — console.seed.run/orgs/_your-org-name_/settings/billing.

1. Make sure the stages that don't need to be auto-deployed are [set to deploy manually]({% link _docs/updating-the-stage-source.md %}#auto-deploy-options). This will decrease the number of deployments your team will be making.
2. Consider not [auto-deploying PRs]({% link _docs/working-with-pull-requests.md %}) and [branches]({% link _docs/working-with-branches.md %}). Deploying (and cleaning up) a new PR or branch stage takes a lot longer than continuing to deploy to a previously deployed stage.
3. You can also turn off auto-deploying for a stage and just [manually deploy specific services]({% link _docs/manually-deploying.md %}#manually-deploy-a-service). This makes a lot of sense if you are working with sensitive infrastructure services.
4. Turn off [individually packaging functions](https://serverless.com/framework/docs/providers/aws/guide/packaging#individual-function-packages). Packaging functions individually reduces the Lambda package size and reduces cold start times. But it also increases build times. So for non performance critical services, turn off individual packaging.  
5. You can also use the [steps in the build log]({% link _posts/2020-02-19-steps-in-the-build-log.md %}) to figure out where most of the time is spent and find ways to reduce that. This also has he added benefit of speeding up your builds.
6. For monorepo apps, Seed uses the Git log and directory structure to figure out which services have change and deploy only those. Make sure your app [is organized to take advantage of this]({% link _docs/incremental-service-deploys.md %}).
7. Move services that are not often updated, to their own app and turn off auto-deploying them. For example, move the services that setup your database tables, S3 buckets, Cognito User Pools or Identity Pools to a separate app. We [recommend this workflow over on Serverless Stack](https://serverless-stack.com/chapters/organizing-serverless-projects.html#a-practical-approach). To do this you won't need to remove the service from AWS and redeploy it. You can simply remove it from an existing app on Seed and add it as a new app.

This isn't an exhaustive list, but it should point you in the right direction.

### Upcoming pricing plan changes

We'll also be rolling out some changes to our pricing plans over the next month to further help you save on your expenses. This will include:

- A discount for paying annually as opposed to monthly,
- An option to add build minutes without increasing the number of seats,
- And a lower price per seat.

This new pricing plan will be made available over the next month. If you are eager to get started with these changes, feel free to [contact us via email](mailto:{{ site.email }}). 

## Summary

We hope this guide helps you manage your costs and usage on Seed. As always you can [contact us directly](mailto:{{ site.email }}) if you need some help.

To end on a brighter note, you might have noticed the [incredibly exciting changes we rolled out recently]({% link _posts/2020-03-13-a-brand-new-dashboard.md %}). We've got a ton more planned on our roadmap for you and we think this is just the beginning of our Serverless journey together. Stay tuned!


