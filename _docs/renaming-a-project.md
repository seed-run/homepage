---
layout: docs
title: Renaming a Project
---

Seed projects have a couple of identifiers that can help you organize and share your projects.

- **Project Name**

  This is what you see in the console and it is only visible to you. So if you add a project member and you change your project name, they will not see the change you made. The project name is useful for organizing your various serverless projects. You can even use Emojis in your project name.

- **Project Slug**

  This is a globally unique id that Seed uses to identify your project. This is also used in the URL to make them easy to read. And when you add project members they'll see this as a part of the project URL as well. Any changes made to the project slug are visible to all the project members.

For example, your project name might be "My Serverless Project" and your project slug could be "my-serverless-project". The project URL in this case would be `https://console.seed.run/projects/my-serverless-project`. The slug needs to be globally unique but the name can be set to anything you like.

> Project names are just for you, whereas project slugs are visible to your team

When you first add your project, we set these based on the git repository that is being added. But you can change them from your project settings.

![Project Info](/assets/docs/renaming-a-project/project-info.png)

The project name and slug in combination can help you organize your project while creating easy to read/share URLs.
