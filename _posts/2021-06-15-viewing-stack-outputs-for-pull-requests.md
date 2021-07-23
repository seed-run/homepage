---
layout: post
title: Viewing stack outputs for Pull Requests
categories: news
author: frank
---

Seed will add comments in your PRs with the stack outputs from the services that have been deployed.

![Seed PR comment with stack outputs](/assets/blog/viewing-stack-outputs-for-pull-requests/seed-pr-comment-with-stack-outputs.png)

Previously, if you were [auto-deploying PRs]({% link _docs/working-with-pull-requests.md %}), Seed would add a comment in your PR with the deployed API endpoint. Now, Seed will show the entire stack output from all the services in your app. You can expand the details in the comment by clicking **View stack outputs**. 

You can also optionally disable this behavior from the PR settings. Make sure to uncheck the **Add a PR comment with the stack outputs** option.

![Disable Seed PR stack outputs comment](/assets/blog/viewing-stack-outputs-for-pull-requests/disable-seed-pr-stack-outputs-comment.png)

Read more about this over on our docs on [Working with pull requests]({% link _docs/working-with-pull-requests.md %}).
