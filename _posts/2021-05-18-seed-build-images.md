---
layout: post
title: Seed Build Images
categories: news
author: jack
---

The build images used in Seed are now hosted on [Docker Hub](https://hub.docker.com/r/seedrun/build/tags).

![Seed build images in Docker Hub](/assets/blog/seed-build-images/seed-build-images-in-docker-hub.png)

Seed uses a set of [build images]({% link _docs/seed-build-images.md %}) to deploy your services. These are automatically selected based on the runtime of the service being deployed.

However, sometimes you might run into some build issues that require you to test things locally. Now you can; by using the images that we've hosted on Docker Hub — [**seedrun/build**](https://hub.docker.com/r/seedrun/build/tags)

Make sure to [read the docs]({% link _docs/seed-build-images.md %}#running-locally) and [reach out](mailto:{{ site.email }}) if you need any help.
