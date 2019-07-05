---
layout: post
title: Improved Code Fetching
image: /assets/social-cards/building-artifacts-concurrently.png
categories: news
author: jack
---

We've rolled out a few changes to the way the source code for your projects is fetched. Making the process almost 70% faster.

This means that your should see a noticeable improvement with your build times. This is especially true for folks with large repositories. Previously, the process could take a minute or two if the git repository for your project was a few GB in size. By changing the way we cache some of the build artifacts we've cut this down by nearly 70%. We've also offloaded a couple of non-critical steps in the build process, further speeding up the process.

Since Seed focusses specifically on Serverless, we are able to figure out the most optimal way to build your apps. This greatly improves the CI/CD process for Serverless projects.
