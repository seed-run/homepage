---
layout: post
title: Introducing the Seed CLI
categories: news
image: assets/social-cards/seed-cli.png
author: jay
---

Seed now has a CLI that allows you to trigger deployments to your apps from anywhere in your organization's workflow. 

<img style="max-width: 486px" alt="Seed CLI npm install" src="/assets/blog/introducing-the-seed-cli/seed-cli-npm-install.png" />

The Seed CLI is available as an [npm package]({{ site.cli_npm }}).

``` bash
$ npm install -g @seed-run/cli
```

You simply need to pass in the org, app, and stage that you want to deploy a specific Git commit to.

``` bash
$ SEED_TOKEN=$ACME_ORG_TOKEN seed deploy \
  --org acme \
  --app backend-api \
  --stage dev \
  --commit 700b9c2
```

The `SEED_TOKEN` can be genrated from your organization's settings.

This allows you to control when you want your serverless apps to be deployed to Seed. You don't need to push a Git commit to do so. This makes it easy to integrate your workflow with Seed.

[Read more about deploying with the Seed CLI over on our docs]({% link _docs/deploying-with-the-seed-cli.md %}).
