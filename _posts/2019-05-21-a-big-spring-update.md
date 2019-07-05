---
layout: post
title: A Big Spring Update
categories: news
author: frank
---

We've rolled out a big update to Seed with a couple of key improvements that we'd like to announce.

![New Seed pipeline UI](/assets/blog/a-big-spring-update/new-seed-pipeline-ui.png)

### A New Pipeline UI

We have an all new pipeline interface that makes it a lot easier to edit and interact with the various aspects of your serverless app.

1. The overall status of a build

   Previously, the pipeline table only showed you the status of each of the services in your app. This meant that you would have to click on a specific build to see its complete status. Now, we show you the status of a build clearly at the top of the stage.

2. Viewing build logs for a service

   Also, clicking on the build status for a service now takes you to the build logs for that specific service.

3. Manually trigger deployments

   You can trigger a deployment to a stage directly from the pipeline without having to click through to it.

   ![Manual deploy modal](/assets/blog/a-big-spring-update/manual-deploy-modal.png)

   Along those same lines, you can trigger a deployment to a specific service directly from the pipeline as well.

   ![Manual deploy service dropdown](/assets/blog/a-big-spring-update/manual-deploy-service-dropdown.png)

4. Promote a service

   While you could promote a stage from the old UI; you still needed to click through to an individual service to promote it. Now you can promote a service by clicking on the dropdown next to it.

   ![Promote service modal](/assets/blog/a-big-spring-update/promote-service-modal.png)

5. Add a service

   You can also add a service directly from the pipeline.

   ![Add service modal](/assets/blog/a-big-spring-update/add-service-modal.png)

6. Edit the pipeline

   Finally, you can edit the pipeline in-place without having to go to the settings page to do so. The pipeline editor allows you to add new dev/staging stages and re-order them as well.

   ![Edit pipeline ui](/assets/blog/a-big-spring-update/edit-pipeline-ui.png)

The new UI improvements gives you a great bird's-eye view of your deployment pipeline and one click access to all the common actions.


### Only Deploy Updated Services

Another big update that we had been working on, is to be able to skip deploying services that haven't changed. Previously, Seed would force deploy all your services on every commit. This meant that for [monorepo serverless apps]({% link  _docs/mono-repo-apps-in-seed.md %}) with [multiple deploy phases]({% link _docs/configuring-deploy-phases.md %}), builds could be really slow.

Now Seed will skip deployments for services that haven't been updated. We rely on the check that Serverless Framework does for this. It diffs the code package and CloudFormation template to see if the service needs to be deployed. Note that, the entire build process proceeds as if the build has been successful. This means that all the relevant [hooks in the build spec]({% link _docs/adding-a-build-spec.md %}) are executed.

Builds that have been skipped are marked as such and you can see their status in the build logs.

![Skipped build logs status](/assets/blog/a-big-spring-update/skipped-build-logs-status.png)

There might be cases where you want to force a deployment. To do this simply select the force option while triggering a deployment.

![Select force option for manual deploy](/assets/blog/a-big-spring-update/select-force-option-for-manual-deploy.png)

You also might have noticed that your builds have gotten faster over the past few weeks. We are doing some great work behind the scenes to improve this. While this will be an ongoing process, we updated the console to show you how long a build took to deploy.

![Build deploy time](/assets/blog/a-big-spring-update/build-deploy-time.png)

You'll notice that we also show you how long each service took to complete.

### Better Git Integration

We also made some changes over the last couple of weeks to add better Git related context to the builds. We now show you the avatar of the committer and the commit message.

![Build activity git context](/assets/blog/a-big-spring-update/build-activity-git-context.png)

And the full commit info as a part of the build report.

![Build report git context](/assets/blog/a-big-spring-update/build-report-git-context.png)

Finally, we allow you to review the code changes while promoting a build.

![Promote service modal](/assets/blog/a-big-spring-update/promote-service-modal.png)

This sends you to GitHub (or your Git provider) to compare the commits.


All the great feedback we've been receiving has really helped shape the product roadmap for Seed. We have a ton of other updates in store. We think this will continue to make Seed the easiest way to manage deployments for your Serverless apps. So give the new updates a try and continue to send us your feedback!
