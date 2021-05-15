---
layout: post
title: Node v14 Support
categories: news
author: frank
---

We recently added Node v14 support in Seed.

### General Purpose v4

The new [General Purpose v4]({% link _docs/seed-build-images.md %}) build image comes with Node.js v14.

You can select the build image by heading over to your [service's settings]({% link _docs/seed-build-images.md %}#changing-the-build-image).

### Customizing versions

Note that these build images come loaded with [n](https://github.com/tj/n). This allows you to select the specific version of Node.js you want. Add the following in your `seed.yml`.

``` yml
before_compile:
  - n 14.17.0
```

You can install the version of npm you want in the same way. For example, if you wanted to use the latest version of npm, add the following.

``` yml
before_compile:
  - npm i -g npm@latest
```

So if you are currently using Node v14, give the above changes a try!
