---
layout: docs
title: Renaming an App
redirect_from: /docs/renaming-a-project.html
---

Apps in Seed have a couple of identifiers that can help you organize and share them.

- **App Name**

  This is what you see in the console and it is only visible to you. So if you add a team member and you change your app name, they will not see the change you made. The project name is useful for organizing your various serverless projects. You can even use Emojis in your app name.

- **App Slug**

  This is a globally unique id that Seed uses to identify your project. This is also used in the URL to make them easy to read. And when you add project members they'll see this as a part of the project URL as well. Any changes made to the project slug are visible to all the project members.

For example, your app name might be "My Serverless Project" and your app slug could be "my-serverless-project". The project URL in this case would be `https://console.seed.run/projects/my-serverless-project`. The slug needs to be globally unique but the name can be set to anything you like.

> App names are just for you, whereas app slugs are visible to your team

When you first add your app, we set these based on the git repository that is being added. But you can change them from the app settings.

![App Info](/assets/docs/renaming-an-app/app-info.png)

The app name and slug in combination can help you organize your project while creating URLs that are easy to read and share.
