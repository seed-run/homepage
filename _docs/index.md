---
layout: docs
title: Getting Started with Seed
description: Documentation for using Seed to build and deploy Serverless apps
---

Seed is a fully-configured code pipeline for building and deploying Serverless apps on AWS. Simply add your Git repository and IAM credentials and your entire team can `git push` to deploy updates to your Serverless app.

Seed currently supports the following:

- [Serverless Framework](https://serverless.com/framework/) projects
- Built for [Node.js](https://nodejs.org/en/) and [Python](https://www.python.org)
- Deployed to [AWS](https://aws.amazon.com)
- Hosted on [GitHub](https://github.com), [Bitbucket](https://bitbucket.org/), and [GitLab](https://gitlab.com)

Support for other platforms and repositories are coming soon. [Send us an email](mailto: {{ site.email }}) to let us know what you would like us to support next.

### Prerequisites

Seed needs very little configuration on your part and there is no CLI to install. But to add your project you need to:

1. Add your project repository with your Git provider
2. Create an IAM Role for your AWS account
3. Optionally, specify the location of the default service in your repo.

![Create a new app](/assets/docs/create-a-new-app.png)

Let's get started with adding your project to the [Seed Console]({{ site.console_url }}/new) by taking a look at how to create a an [AWS IAM Role]({% link _docs/adding-your-iam-credentials.md %}). 
