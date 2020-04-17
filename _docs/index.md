---
layout: docs
title: Getting Started with Seed
description: Documentation for using Seed to build and deploy Serverless apps
---

Seed is a fully managed CI/CD pipeline for Serverless apps on AWS. Simply add your Git repository and IAM credentials and your entire team can `git push` to deploy updates to your Serverless app.

Seed currently supports the following:

- [Serverless Framework](https://serverless.com/framework/) projects deployed to [AWS](https://aws.amazon.com)
- Built with [Node.js]({% link _docs/adding-nodejs-projects.md %}), [Python]({% link _docs/adding-python-projects.md %}), [.NET Core]({% link _docs/adding-dotnet-core-projects.md %}), [Go]({% link _docs/adding-go-projects.md %}), [Ruby]({% link _docs/adding-ruby-projects.md %}), and [Java]({% link _docs/adding-java-projects.md %}).
- Hosted on [GitHub](https://github.com), [GitHub Enterprise]({% link _docs/enabling-github-enterprise.md %}), [Bitbucket](https://bitbucket.org/), [GitLab](https://gitlab.com), and [GitLab Self-Managed]({% link _docs/enabling-gitlab-self-managed.md %}).

Support for other platforms and repositories are coming soon. [Send us an email](mailto: {{ site.email }}) to let us know what you would like us to support next.

### Prerequisites

Seed needs very little configuration on your part and there is no CLI to install. But to add your project you need to:

1. Add your project repository with your Git provider
2. Create an IAM Role for your AWS account

To start with, Seed will ask you to create a new app by adding your project from your repository.

![Create a new app](/assets/docs/index/create-a-new-app.png)

Once you select your Git provider (GitHub for example), you'll be asked to login to your Github.

![Login to GitHub](/assets/docs/index/login-to-github.png)

Here you'll be asked to authorize Seed. Make sure to select the **Repositories** and **Organization access** you need.

![Authorize Seed on GitHub](/assets/docs/index/authorize-seed-on-github.png)

Once authorized, you can select your repo. Seed will look for all the `serverless.yml` files in your repo.

If you are unable to find your repo, it might be because Seed doesn't have the permissions to access your repo. You can [read about how to fix this here]({% link _docs/cannot-find-my-repo.md %}).

![Auto-detect serverless.yml for new app](/assets/docs/index/auto-detect-serverless-yml-for-new-app.png)

If detected, you can select to add a service. You can always add other services later.

![Confirm default service for new app](/assets/docs/index/confirm-default-service-for-new-app.png)

If the services could not be detected, you can add it manually.

![Pick different default service for new app](/assets/docs/index/pick-different-default-service-for-new-app.png)

Next, Seed will create a **dev** and **prod** stage (or environment) for your app. Note that, you'll need to change the names to match the stage names you are using to deploy your app. This is important because Seed will deploy your app using the `serverless deploy --stage $STAGE_NAME` command. Here `$STAGE_NAME` is the name.

> Seed deploys to your environments using the stage name.

You also need to configure the stage with the AWS IAM credentials needed to deploy to it. By default, Seed will use the same credentials to deploy to production. You can change this if your production environment is in a different AWS account.

![Configure IAM user for a new app](/assets/docs/index/configure-iam-user-for-new-app.png)

If you've added an app before, you have the option of configuring your new app with the settings of an existing app. Hit the **Copy Settings** tab.

Here you can select one of your existing apps.

![Select existing app settings for new app](/assets/docs/index/select-existing-app-settings-for-new-app.png)

> A personal app can only inherit the settings from another personal app. And the same applies to organization apps.

Next, let's look at how to create an [AWS IAM User]({% link _docs/adding-your-iam-credentials.md %}).
