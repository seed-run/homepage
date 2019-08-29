---
layout: post
title: Add an SSH key to your builds
categories: news
author: jack
---

Seed now supports adding a private SSH key to your build processes. You can add an SSH key for your organization and Seed will use it for all the builds across all your apps.

![Add an SSH key for your organization](/assets/blog/add-an-ssh-key-to-your-builds/add-an-ssh-key-for-your-organization.png)

Once you added, Seed will add the key to the `~/.ssh/id_rsa` file in your build processes. This will allow you to checkout other repos or run any other operations that rely on SSH.

You can read more about this in our docs — [**Adding an SSH key for your organization**]({% link _docs/adding-an-organization-ssh-key.md %}).
