---
layout: post
title: Phasing out Issues
categories: news
author: jay
---

We are planning to phase out the Issues feature over the coming year.

### Background

[Issues in Seed]({% link _docs/issues-and-alerts.md %}) allows you to monitor your serverless apps for free. Over the last couple of months we added support for [Issues to the SST Console](https://docs.sst.dev/console#issues) as well.

### Why we are doing this

There are a couple of reasons why we are planning to phase out Issues in Seed.

- With the SST Console, we can support things like source maps right out of the box since it's more tightly coupled to SST apps.
- The two services are currently redundant and it doesn't make sense for us to support them in both places.
- While this does leave out Serverless Framework users. It's worth noting that starting with v4, [Serverless Framework is moving away from a free open source model to a paid one](https://www.serverless.com/blog/serverless-framework-v4-a-new-model). Ever since the announcement we've been seeing folks in our community migrate away from it.

### How we are doing it

We are going to phase out Issues in two steps. First by turning it off for inactive users, and then for everybody. Here's what it's going to look like:

1. Step 1: **Disabled for inactive users** (Jan 3rd, 2024)
   - Issues will be **temporarily disabled** for apps that haven't been actively using it (no resolved or ignored issues in the past 30 days).
   - However, you can still **re-enable it** from your app settings.
   - Once re-enabled, Issues will continue to work as before.

2. Step 2: **Disabled for everybody** (Jun 3rd, 2024)
   - We'll be turning off Issues for all apps.
   - We are setting a tentative date of June 3rd, 2024. We'll announce the exact date in the coming weeks.

If you have any questions or need additional time with the migration, [make sure to contact us](mailto:contact@seed.run).
