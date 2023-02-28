---
layout: post
title: SST v2 support
categories: news
author: jay
---

Seed now supports SST v2, Node 16, and pnpm out of the box.

Now that [SST v2 is officially out](https://sst.dev/blog/sst-v2.html), we are happy to announce that you can deploy SST v2 directly through Seed.

SST v2 also defaults to Node 16 and supports [pnpm](https://pnpm.io); so Seed supports this as well! If Seed detects a `pnpm-lock.yaml` it'll use pnpm as the package manager for the build.

If you are upgrading to SST v2, make sure to [check out the upgrade guide over on the SST docs](https://docs.sst.dev/upgrade-guide#upgrade-to-v20).
