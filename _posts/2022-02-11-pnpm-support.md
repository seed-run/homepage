---
layout: post
title: pnpm support
categories: news
author: jay
---

Seed now supports checking for code changes using the [pnpm](https://pnpm.io) package manager. 

[pnpm](https://pnpm.io) is a faster package manager that works great for monorepo projects. You can enable incremental service deployments if you are using [pnpm Workspaces](https://pnpm.io/workspaces). Seed can use pnpm to figure out if a service has been updated in the commits that have been pushed.

Enable it by adding the following to your `seed.yml`.

``` yaml
check_code_change: pnpm
```

[Read more about this]({% link _docs/incremental-service-deploys.md %}#use-pnpm-to-check-updated-packages) over on the docs.
