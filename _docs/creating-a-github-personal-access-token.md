---
layout: docs
title: Creating a GitHub Personal Access Token
---

[Seed](/) uses your GitHub Personal Access Token to access your project repository. Use the following instructions from GitHub to create your Personal Access Token.

&rarr; [`Creating a personal access token`](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)

On **Step 6** while selecting the scopes for the token, make sure to select the **repo** and **admin:repo_hook** options as shown below.

![Select GitHub Personal Access Token Scopes Screenshot](/assets/docs/select-github-personal-access-token-scopes.png)

Seed needs these to access your repository and to add a Webhook to keep track of commits to your repository.

Copy your **GitHub Personal Access Token** and add it while [creating a new project]({{ site.console_url }}/new).
