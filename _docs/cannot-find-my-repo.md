---
layout: docs
title: Cannot Find My Repo
---

#### Problem

You might have successfully authenticated with your Git provider but you are unable to see your repo in the list. This usually happens either if the Seed GitHub app has not been added to your organization. Or if Seed does not have access to the given repo.

#### The Fix

First make sure the Seed GitHub app has been added. If you are adding a personal app, head over to your settings on GitHub and check the **Applications** section.

![Application settings for personal GitHub account](/assets/docs/cannot-find-my-repo/application-settings-for-personal-github-account.png)

For repos in your organization, head over to the **Installed GitHub Apps** section in your organization's settings.

![Installed GitHub apps in GitHub organization](/assets/docs/cannot-find-my-repo/installed-github-apps-in-github-organization.png)

If you don't find Seed installed in your organization, you can add it back in the Seed console. Hit the **Add an organization…** button and configure your organization.

![Add Seed to GitHub organization](/assets/docs/cannot-find-my-repo/add-seed-to-github-organization.png)

Next, hit the **Configure** button next to the Seed GitHub app to view its settings. Here you need to make sure that you have given the Seed app permission to the repo you are trying to add.

![Repository access for Seed app in GitHub](/assets/docs/cannot-find-my-repo/repository-access-for-seed-app-in-github.png)

Now over on Seed, you should be able to find your repo once you refresh and authenticate with GitHub.

If you are still having problems, feel free to [contact us](mailto:{{ site.email }}).
