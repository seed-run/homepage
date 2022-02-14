---
layout: post
title: pnpm support
categories: news
author: jay
---

Seed now supports the [pnpm](https://pnpm.io) package manager. This includes support for incremental service deployments as well. 

[pnpm](https://pnpm.io) is a faster package manager that works great for monorepo projects. Seed now has out of the box support for deploying repos that use pnpm.

In addition, you can also enable incremental service deployments if you are using [pnpm Workspaces](https://pnpm.io/workspaces). Seed can use your package manager to figure out if a service has been updated in the commits that have been pushed.

Enable it by adding the following to your `seed.yml`.

``` yaml
check_code_change: pnpm
```

[Read more about this]({% link _docs/incremental-service-deploys.md %}#use-pnpm-to-check-updated-packages) over on the docs.
