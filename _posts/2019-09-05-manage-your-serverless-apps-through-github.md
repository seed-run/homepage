---
layout: post
title: Manage your Serverless apps through GitHub
image: assets/social-cards/seed-github.png
categories: news
author: jay
---

We've got some really exciting improvements to our GitHub integration that we'd like to announce. You can now manage your Serverless deployments almost entirely from your GitHub repo!

Let's quickly look at how it works.

#### Environments

You can see all the stages your Serverless app is deployed to by clicking on the environments tab in your GitHub repo.

![Seed stages listed in GitHub](/assets/blog/manage-your-serverless-apps-through-github/seed-stages-listed-in-github.png)

Here you have 1-click access to all the stages on Seed and the most recent build in that stage.

You can also view your deployment history from here.

![Seed deployment history in GitHub](/assets/blog/manage-your-serverless-apps-through-github/seed-deployment-history-in-github.png)

This gives you a clear view of which builds failed and the commits associated with them.

#### Pull Requests

For pull requests, you can view the deployment progress of your monorepo Serverless app.

![Seed PR building check in GitHub](/assets/blog/manage-your-serverless-apps-through-github/seed-pr-building-check-progress-in-github.png)

And after a deployment completes, the deployed endpoints are readily available to you along with the newly deployed stage.

![Seed PR complete info in GitHub](/assets/blog/manage-your-serverless-apps-through-github/seed-pr-complete-info-in-github.png)

#### Status Checks

Status checks like the one above are also available for all your commits.

![Seed commit status checks in GitHub](/assets/blog/manage-your-serverless-apps-through-github/seed-commit-status-checks-in-github.png)

#### Branch Protection Rules

This allows you to protect certain branches by adding a rule based on the status checks.

![Seed branch protection status checks in GitHub](/assets/blog/manage-your-serverless-apps-through-github/seed-branch-protection-status-checks-in-github.png)

#### GitHub Slack App

Finally, you can subscribe to the build notifications via the [GitHub Slack app](https://slack.github.com).

<div style="text-align: center">
  <img style="margin: 15px 0 30px; box-shadow: 0 15px 35px rgba(0,0,0,.1),0 5px 15px rgba(0,0,0,.04)" alt="Seed build info in GitHub Slack app" src="/assets/blog/manage-your-serverless-apps-through-github/seed-info-in-github-slack-app.png" width="426" />
</div>

### How to upgrade

The new and improved GitHub integration is live and you just need to connect your GitHub repo to Seed. If you are currently using GitHub with Seed, you'll need to reconnect your repo through the Seed app settings. Note that, the environments info in GitHub will populate as you deploy to the various stages.

---

You can read about these workflows in detail in our docs:

- [GitHub integration]({% link _docs/github-integration.md %})
- [Working with pull requests]({% link _docs/working-with-pull-requests.md %})

We want Seed to fit seamlessly with your workflow and we think these improvements to our GitHub integration go a long way in doing that.
