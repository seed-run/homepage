---
layout: page
title: Getting Started with Seed
description: Documentation for using Seed to build and deploy Serverless apps
---

Seed is a fully-configured code pipeline for building and deploying Serverless apps on AWS. Simply add your GitHub repository and IAM credentials and your entire team can `git push` to deploy updates to your Serverless app.

Seed currently supports the following:

- [Serverless Framework](https://serverless.com/framework/) projects
- Built with [Node.js](https://nodejs.org/en/)
- Deployed to [AWS](https://aws.amazon.com)
- Hosted on [GitHub](https://github.com)

Support for other platforms and repositories are coming soon. [Send us an email](mailto: {{ site.email }}) to let us know what you would like us to support next.

### Pre-requisites

Seed needs very little configuration on your part and there is no CLI to install. But before we get started with setting up your project ensure that you can create a:

1. Personal access token for your GitHub repo
2. IAM Role for your AWS account

![Create a new project](/assets/docs/create-a-new-project.png)

Let's get started with adding your project to the [Seed Console]({{ site.console_url }}/new) by taking a look at how to create a [GitHub personal access token]({% link _docs/creating-a-github-personal-access-token.md %}) and an [AWS IAM Role]({% link _docs/adding-your-iam-credentials.md %}). 
