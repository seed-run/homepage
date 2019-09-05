---
layout: docs
title: GitHub Integration
---

[Seed](/) integrates really well with GitHub. In this chapter we'll look at the various points of integration.

### Environments

GitHub also has a tab to view your [environments](https://help.github.com/en/articles/viewing-deployment-activity-for-your-repository) that Seed integrates with. This means that you can see all your environments and deployment history right in GitHub!

> You can see all your environments and deployment history right in GitHub!

Click on the **environments** tab in your repo.

![GitHub repo environments tab](/assets/docs/github-integration/github-repo-environments-tab.png)

Here you'll notice all your environments/stages listed at the top. You can do a couple of things here:

- The **View deployment** button will take you to the stage in Seed.
- And the **deployed** link near the commit will take you to that specific build.

![Seed stages listed in GitHub](/assets/docs/github-integration/seed-stages-listed-in-github.png)

Scroll down a bit further on this page and you can see your entire deployment history on Seed.

![Seed deployment history in GitHub](/assets/docs/github-integration/seed-deployment-history-in-github.png)

This is incredibly useful because it allows you to filter by environments. You can also click the **Deployed** link to see why that commit failed to build.

### Pull Requests

We have [a detailed chapter on working with pull requests]({% link _docs/working-with-pull-requests.md %}), but we'll touch on how Seed integrates with GitHub.

You can view the deployment status of your PR right from GitHub.

![Seed PR building check in GitHub](/assets/docs/github-integration/seed-pr-building-check-progress-in-github.png)

Once complete, Seed will add some useful info about the deployment.

![Seed PR complete info in GitHub](/assets/docs/github-integration/seed-pr-complete-info-in-github.png)

In the above screenshot:

1. Seed will add a comment with a list of any deployed API endpoints. This is useful for cases where you have a frontend application that needs to be tested against this endpoint.

2. And the **View deployment** button in the environments section takes you to the deployed stage in Seed.

Also, if the PR fails to deploy, the **Details** link will take you straight to the build logs on Seed.

![Seed PR building failed in GitHub](/assets/docs/github-integration/seed-pr-building-failed-in-github.png)

### Status Checks

The above checks are also available for all commits. 

![Seed commit status checks in GitHub](/assets/docs/github-integration/seed-commit-status-checks-in-github.png)

### Branch Protection Rules

You can also use these checks to set up [branch protections rules](https://help.github.com/en/articles/configuring-protected-branches). For example, you might want all the PR related checks to run before merging to your _master_ branch. To do this, simply enable the **seed: pr** check.

![Seed branch protection status checks in GitHub](/assets/docs/github-integration/seed-branch-protection-status-checks-in-github.png)

### GitHub Slack App

Finally, you can subscribe to the build notifications via the [GitHub Slack app](https://slack.github.com).

<div style="text-align: center">
  <img style="margin: 15px 0 30px; box-shadow: 0 15px 35px rgba(0,0,0,.1),0 5px 15px rgba(0,0,0,.04)" alt="Seed build info in GitHub Slack app" src="/assets/docs/github-integration/seed-info-in-github-slack-app.png" width="426" />
</div>

---

Seed's GitHub integration is designed to fit perfectly with your current workflow! And it makes it really easy to work with Serverless apps.
