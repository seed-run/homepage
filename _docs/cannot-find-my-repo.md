---
layout: docs
title: Cannot Find My Repo
---

#### Problem

You might have successfully authenticated with your Git provider but you are unable to see your repo in the list. This usually happens when Seed doesn't have the right permissions; either to your private repositories or your organizations.

#### The Fix

To fix this, head over to your GitHub settings.

![Click GitHub settings](/assets/docs/cannot-find-my-repo/click-github-settings.png)

From the sidebar, click **Applications**.

![Click Applications in GitHub sidebar](/assets/docs/cannot-find-my-repo/click-applications-in-github-sidebar.png)

And select **Authorized OAuth Apps** from the tabs at the top.

![Click Authorized OAuth Apps in GitHub](/assets/docs/cannot-find-my-repo/click-authorized-oauth-apps-in-github.png)

Look for **Seed** in the list and click through.

![Click on Seed in GitHub settings](/assets/docs/cannot-find-my-repo/click-on-seed-in-github-settings.png)

Here, make sure the **Permissions** and **Organization access** are correctly granted for the repo you are looking to add.

![Set Seed permissions in GitHub settings](/assets/docs/cannot-find-my-repo/set-seed-permissions-in-github-settings.png)

Now over on Seed, you should be able to find your repo once you refresh and authenticate with GitHub. If you are still having problems, feel free to [contact us](mailto:{{ site.email }}).
