---
layout: post
title: Transitioning to npm 7
categories: news
author: frank
---

Seed will now automatically use npm 7 if it detects the new lockfile format.

[npm 7 has a couple of breaking changes](https://github.blog/2021-02-02-npm-7-is-now-generally-available/), including a new lockfile format. This means that the new lockfile is incompatible with previous versions of npm. To help with this transition, if Seed detects the newer lockfile format, it'll automatically use npm 7 to install the dependencies.

Read more about [adding Node.js serverless apps]({% link _docs/adding-nodejs-projects.md %}) over on our docs.
