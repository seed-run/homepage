---
layout: post
title: Adding App Specific Roles
categories: news
author: jack
---

Seed now allows you to add App Specific Roles. This allows you to restrict access to certain sensitive apps in your org.

![App specific role based access control in Seed](/assets/blog/adding-app-specific-roles/app-specific-role-based-access-control-in-seed.png)

By default, member roles in Seed apply to all the apps in your organization. However, there might be cases where you want to restrict access to certain apps. It might be because it's deploying some key pieces of your infrastructure.

Now you can do so by adding app specific roles. You'll be required to select the app and the modified role you want applied.

![Selecting app specific role in Seed](/assets/blog/adding-app-specific-roles/selecting-app-specific-role-in-seed.png)

Note that, the app specific role overrides the default role you have assigned for the org.

Role-based access controls (RBAC) are a great way to secure access to your production environments. And App Specific Roles now allow you to extend that to specific apps in your org as well. For further details, check out [our doc on adding members to your organization]({% link _docs/adding-organization-members.md %}).

_RBAC and App Specific Roles are a part of our Enterprise plan. To find out more, or to upgrade your plan; [head over to our pricing page]({% link pricing.html %})_.
