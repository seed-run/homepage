---
layout: post
title: Seed and SST v3
categories: news
author: jay
---

You might've seen the announcement that [SST v3](https://sst.dev/blog/sst-v3) is out.

SST v3 is a major change and doesn't use CDK or CloudFormation. Instead it uses Pulumi and Terraform. You can [read more about our decision to move away from it](https://sst.dev/blog/moving-away-from-cdk).

Seed, as you might know, supports deploying [CDK apps built with SST]({% link _docs/adding-a-cdk-app.md %}) and Serverless Framework apps. Both of these are utlimately built on CloudFormation.

This makes it pretty tricky to support SST v3 on Seed. As a result, we decided to not add support for it. Instead, the [SST Console](https://sst.dev/docs/console/) can [auto-deploy](https://sst.dev/docs/console/#autodeploy) your SST v3 apps.

> Seed does not support deploying SST v3 apps.

Seed is still going to be around and will be kept up to date. But as you migrate from v2 to v3, we recommend migrating over to the SST Console.

[You can learn more about migrating to the SST Console](https://sst.dev/docs/migrate-from-v2#cicd).
