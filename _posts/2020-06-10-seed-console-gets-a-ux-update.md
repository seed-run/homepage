---
layout: post
title: Seed Console Gets a UX Update
categories: news
author: jay
image: assets/social-cards/seed-console-ux-update.png
tweet: https://twitter.com/SEED_run/status/1271055270295359489
---

Today we are rolling out a major design update to the Seed console. In this post we'll be going over the changes that are a part of this update.

### Background

A few weeks ago we ran a survey asking for some feedback on [the dashboard]({% link _posts/2020-03-13-a-brand-new-dashboard.md %}) that we released back in March. One of the biggest pieces of feedback we received revolved around the UI of the Seed console. A lot of you found it confusing to navigate around, especially when looking to change the settings of the app. You also felt that it took too many clicks to get to commonly used features.

Internally, this has been on our radar for quite a while. The Seed console has slowly outgrown the original layout and structure. It was time for a much needed redesign.

### The New Design

Here's a quick comparison of the Seed console homepage.

![New Seed console homepage](/assets/blog/seed-console-gets-a-ux-update/new-seed-console-homepage.png)
*The new Seed console homepage!*

![Old Seed console homepage](/assets/blog/seed-console-gets-a-ux-update/old-seed-console-homepage.png)
*Compared to the old Seed console homepage.*

#### Common Actions

The first thing you'll notice about the new design is that there is a bigger focus on the most commonly carried out actions. This is a pattern that is applied across all of our pages. Also, it makes much better use of the screen real estate.

#### Navigation

To address the issues around navigation, the new design has a persistent tab-based navigation for the organization pages.

![Tabs in org pages in Seed](/assets/blog/seed-console-gets-a-ux-update/tabs-in-org-pages-in-seed.png)

And in the apps.

![Tabs in app pages in Seed](/assets/blog/seed-console-gets-a-ux-update/tabs-in-app-pages-in-seed.png)

#### Breadcrumbs

In the previous design the breadcrumbs were a constant feature of the UI. While they were ever-present, they were not contextual and did not help you find your way around specific sections of the console.

For example, the navigation below doesn't give you a good sense of where you are in the app.

![Breadcrumbs in old design](/assets/blog/seed-console-gets-a-ux-update/breadcrumbs-in-old-design.png)

Whereas, in the new UI:

![Contextual breadcrumbs in new design](/assets/blog/seed-console-gets-a-ux-update/contextual-breadcrumbs-in-new-design.png)

The breadcrumbs along with the tab-based navigation give you a clear sense of your place within the console. And the contextual breadcrumbs help you navigate within it.

#### App Settings

The app settings have been revamped in this update. The first thing of note here is that all the settings (stages and services) are a part of the app settings. And can be **accessed in a single click** from any part of the app.

![App settings in new design](/assets/blog/seed-console-gets-a-ux-update/app-settings-in-new-design.png)

This means that you won't have to click around to find that specific setting.

And many of the settings now feature a more intuitive, edit-in-place UI.

![Settings with edit-in-place UI](/assets/blog/seed-console-gets-a-ux-update/settings-with-edit-in-place-ui.png)

#### Managing Pipelines

Seed does a great job of helping you manage the deployment pipelines for your Serverless apps. And this design brings that into focus.

![Pipeline page in new design](/assets/blog/seed-console-gets-a-ux-update/pipeline-page-in-new-design.png)

Here you get a clear view of the:

- Current state of the pipeline
- The Git repo that your app is connected to
- The deploy phases for your services
- And the auto-deploy settings

You'll notice that **clicking on the stage** now takes you to **the build activity** for that stage.

On the other hand, editing the pipeline gives you easy access to everything you need to configure your pipelines.

![Edit pipeline page in new design](/assets/blog/seed-console-gets-a-ux-update/edit-pipeline-page-in-new-design.png)

Here clicking on the stages, takes you directly to the settings for that stage.

#### Deploy Phases

A key part of the pipelines in Seed are the [deploy phases]({% link _docs/configuring-deploy-phases.md %}) and [post-deploy phases]({% link _docs/adding-a-post-deploy-phase.md %}). Previously, you had to configure them in separate parts of the console.

This new design brings them together. You can manage your deploy phases right from your pipeline.

![Manage deploy phases in new design](/assets/blog/seed-console-gets-a-ux-update/manage-deploy-phases-in-new-design.png)

On the same screen, you can configure a **post-deploy phase for all your stages**!

![Configure post-deploy phases in new design](/assets/blog/seed-console-gets-a-ux-update/configure-post-deploy-phases-in-new-design.png)

No more having to go from stage to stage to set it up.


#### Bonus

You might have noticed one new tab in your app pages — Issues!

We've got something amazing in store for you. But it needs [**its own announcement**]({% link _posts/2020-06-10-issues-beta.md %})!

### Closing

A big thanks to everybody for their amazing feedback. We hope this new update addresses the concerns (and frustrations) of the old Seed console. We would love for you to try it out and share your feedback with us. Feel free to contact us via the in-app chat or [send us an email](mailto:{{ site.email }}).
