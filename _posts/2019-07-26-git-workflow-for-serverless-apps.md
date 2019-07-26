---
layout: post
title: Git workflow for Serverless apps
image: assets/social-cards/serverless-git-workflow.png
description: In this post we are going to look at some of the most common Git workflows for Serverless apps. We'll cover the simple Git workflow, the manual approval workflow, the feature branch workflow, and finally the PR workflow.
categories: tips
author: frank
---

In this post we are going to look at some of the most common Git workflows for Serverless apps. We'll cover some of the best practices when it comes to Git workflows and see how it works with respect to Serverless.

A couple of things to keep in mind when it comes to thinking about the Git workflow for Serverless specifically.

- Pay per use = multiple dev environments

  Serverless apps and their associated services (Lambda, API Gateway, DynamoDB, etc.) all have a pay per use model. And it seems very likely that more AWS services are moving towards that model. Also, thanks to the [infrastructure as code](https://serverless-stack.com/chapters/what-is-infrastructure-as-code.html) idea that Serverless uses, it is very easy to replicate environments. So creating multiple dev/staging environments is something that is highly recommended.

- Take extra care with infrastructure changes

  Deployments in Serverless apps include both the code and the infrastructure. A downside to this approach is that while reverting code can be easy, reverting infrastructure changes isn't as easy. For example, you can drop a table easily thanks to the infrastructure as code approach. And while you can revert this change and add the table back, restoring the data isn't as straightforward. So it's good to be cautious when it comes to releasing infrastructure changes to production.

Now let's look at some of the most common Git workflows and how they relate to Serverless apps.

### 1. Simple Git workflow

Let's start with the simplest (and perhaps the most common) Git workflow. It looks something like this:

1. The `master` branch auto deploys to _Production_.
2. Your developers work in other dev branches where commits are never directly made to the `master` branch.
3. A common dev branch, let's call it `dev` represents your _Development_ environment.
4. Once you are ready to release to production, you merge commits into `master`.

Here is an easy way to visualize this:

```
DEVELOPMENT  > PRODUCTION
------------   ----------
:dev           :master
```

This simple workflow works best when you have a small team or if you are an individual developer. You only need one dev environment and you know exactly what is going to get promoted to production. The obvious downside to this approach is that there isn't a whole lot of protection around commits to production.

Note that, Seed does not default to this workflow but you can enable this by setting your production stage to [auto-deploy on commits to master]({% link _docs/updating-the-stage-source.md %}).

### 2. Manual approval workflow

Once your team gets a little larger or if you want to be more careful around what gets promoted to production, it's better to apply a manual approval step to your workflow. The workflow is similar to the one above:

1. _Development_ environments are auto-deployed from a Git branch, say `master`.
2. _Production_ environments are not auto-deployed.
3. When releasing to production, the team lead reviews the diff of all the code changes.
4. Also generates a [CloudFormation change set](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/using-cfn-updating-stacks-changesets.html) comparing what is currently running in the _Production_ and what is about to be deployed. Reviewing the change set as a part of the approval process.
5. Approved changes get manually promoted to production.

Let's visualize the workflow:

```
DEVELOPMENT > PRODUCTION (manual promote)
-----------
:master
```

Similar to the Simple Git workflow, you are using two environments/stages. However, your production is never auto-deployed to. This is the setup that Seed defaults to using. As an aside, the [change sets that Seed generates]({% link _docs/promoting-to-production.md %}) are far more readable than the standard CloudFormation change sets. 

### 3. Feature branch workflow

As your team grows, it's likely that you'll be working on multiple features for your product at the same time. This means that you are likely to need multiple _development_ environments. With Serverless this is really easy to do. This workflow looks something like:

1. A new stage/environment is automatically created when a new branch is created.
2. The stage is usually named after the name of the feature branch.
3. When commits are pushed to the feature branch, they are auto-deployed to the connected stage.
4. This means that each feature branch (and accompanying stage) has a complete stack with an API endpoint (if your stack has one) to test with.
5. The feature branches are merged into `master`. It's likely that `master` is tied to a staging environment. Or something that resembles _Production_ as closely as possible.
6. Remove the stage once the feature branch is deleted.
7. This of course can result in many short-lived branches. So make sure that the deployed resources are removed from your AWS account.

If we were to visualize this flow, it might looks something like this:

```
DEVELOPMENT DEVELOPMENT DEVELOPMENT > STAGING > PRODUCTION (manual promote)
----------- ----------- -----------   -------
:feature-a  :feature-b  :feature-c    :master
```

It's recommended that with this setup you host your environments in separate AWS accounts. Refer to our posts on [why you should do this]({% link _posts/2019-07-19-why-deploy-your-serverless-app-into-multiple-aws-accounts.md %}) and [some details on how to do this]({% link _posts/2019-07-24-how-to-deploy-your-serverless-app-into-multiple-aws-accounts.md %}). So in this case you might have three separate AWS accounts. One for all your dev environments, one for your staging, and one for your production environment. You can set these up in [Seed fairly easily as well]({% link _docs/iam-credentials-per-stage.md %}).

Note that, traditional CI systems do not usually monitor branch deletion, Seed does this out of the box and will remove all the resources associated with a stage. And it handles any remove failures gracefully as well. To use this workflow in Seed, simply turn on the [**Enable Auto-Deploy Branches**]({% link _docs/working-with-branches.md %}) feature in your app settings.

### 4. PR Workflow

One of the issues with the Feature branch workflow is that as your team grows, a single _Staging_ environment can be too limiting. If you are using this to do your final integration tests before promoting to production, you are likely to be blocked if other feature branches also need to be approved. To fix this, it's recommended that you merge your changes with a pull request (or PR) to create preview environments/stages. This is what the workflow might look like:

1. You work in a feature branch that is tied to its own unique _Development_ environment.
2. The stage is usually named after the number of the PR (ie. `pr215`).
3. Each preview stage has the complete stack and API endpoint (if it has one) to test with.
4. When commits are added to the pull request, you temporarily merge the source branch and the upstream branch (in this case `master`), and deploy the merged version to the PR stage. This means that your PR stages, give you a _Preview_ of what is about to be deployed.
5. If everything looks good in the PR (or preview) stage, then merge the PR.
6. The _Preview_ stage and all its resources are removed once the PR is closed.
7. Finally, you can promote your _Staging_ environment manually to _Production_. We still recommend a manual step, since it is good to review any infrastructure changes that you are about to make to _Production_.

To visualize this process, your workflow might look something like this.

```
DEVELOPMENT DEVELOPMENT PREVIEW PREVIEW > STAGING > PRODUCTION (manual promote)
----------- ----------- ------- -------   -------
:feature-a  :feature-b  :pr215  :pr216    :master
```

Just as the Feature branch workflow, we recommend using multiple AWS accounts for your environments. Your _Development_ and _Preview_ stages might be in one AWS account, while your _Staging_ and _Production_ environments are in two different AWS accounts.

Note that, with traditional CI systems you usually need to do some extra scripting to set up the PR workflow; Seed does this out of the box and will remove all the resources associated with a preview stage as well. To use this workflow in Seed, simply turn on the [**Enable Auto-Deploy PRs**]({% link _docs/working-with-pull-requests.md %}) feature in your app settings.

#### Summary

This post should give you a really good idea of the different type of Git workflows that are common for Serverless apps. We recommend choosing one that works better for the size of your team. It doesn't make a whole lot of sense to use a very complicated workflow if you are a single developer working on a weekend project. That said, it's fairly easy to move through the various workflows listed above. And of course with [Seed](/) you can set one up in a couple of clicks!
