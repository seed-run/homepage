---
layout: post
title: Fine-Grained Roles
categories: news
author: frank
---

Seed now allows you to have finer control over the roles granted to the members of your organization.

![Fine-grained role based access control in Seed](/assets/blog/fine-grained-roles/fine-grained-role-based-access-control-in-seed.png)

Previously, members in your organization could have restricted access to specific types of stages:

- Development
- Staging
- Production

However, there was no way to grant granular access. This recent update addresses that!

Stage based roles now have the following additional controls:

- **Manage**: Members have access to the settings of a stage.
- **Deploy**: Members can manually deploy to the stage.
- **Promote**: Members can promote to the stage.

This means that you can now allow certain members of your organization to **promote to prod** but **not be able to deploy** (or change any of the settings).

These fine-grained controls are a great way to secure access to your production environments. And allow you to ensure that the right folks on your team have the right type of access. For further details, check out [our doc on adding members to your organization]({% link _docs/adding-organization-members.md %}).

_Note that, role-based access control is a part of our Enterprise plan. To find out more, or to upgrade your plan; [head over to our pricing page]({% link pricing.html %})_.
