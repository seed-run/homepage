---
layout: post
title: Latest Build Images
categories: news
author: frank
---

We rolled out a new version of our build images called the [General Purpose Latest]({% link _docs/seed-build-images.md %}#general-purpose-latest) build image.

As compared to our other images, this one is regularly updated to the latest security patches and runtimes. It's also pre-cached by default on our build machines.

We are making this change to prevent the chance of vulnerable dependencies causing security issues in the build environment.

This image will be used by default for your builds moving forward. If you'd like to pin the runtime or package to a specific version, you can do so through the [build spec]({% link _docs/adding-a-build-spec.md %}). [Read more about this here]({% link _docs/seed-build-images.md %}#general-purpose-latest).

You can still use one of the older build images but note that these are likely to be slower and not as secure.
