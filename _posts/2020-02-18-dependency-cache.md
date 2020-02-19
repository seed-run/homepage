---
layout: post
title: Dependency Cache
image: assets/social-cards/dependency-cache.png
categories: news
author: frank
---

Seed will now automatically cache the dependencies for Node.js projects. This should help make your builds faster!

![Seed restoring cache build log](/assets/blog/dependency-cache/seed-restoring-cache-build-log.png)

The `node_modules` directory will be automatically cached on a per-stage basis. You can [read about this in detail over on our docs]({% link _docs/caching-dependencies.md %}). If you would like support for other runtimes, feel free to [contact us](mailto:{{ site.email }}).

Here is a quick estimate of how much faster your builds can get:

- For **medium** sized projects, it could shave nearly **15 - 20 seconds** of your builds.
- While for some **larger** size projects, could see a speed up nearly **40 - 60 seconds**.

The dependency cache is currently being rolled out to all the _development_ environments for apps on Seed. And it will be turned on for all environments a week from now.
