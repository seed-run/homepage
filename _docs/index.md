---
layout: docs
title: Getting Started with Seed
description: Documentation for using Seed to build and deploy Serverless apps
---

Seed is a fully-configured code pipeline for building and deploying Serverless apps on AWS. Simply add your Git repository and IAM credentials and your entire team can `git push` to deploy updates to your Serverless app.

Seed currently supports the following:

- [Serverless Framework](https://serverless.com/framework/) projects
- Built with [Node.js]({% link _docs/adding-nodejs-projects.md %}), [Python]({% link _docs/adding-python-projects.md %}), [.NET Core]({% link _docs/adding-dotnet-core-projects.md %}), [Go]({% link _docs/adding-go-projects.md %}), and [Ruby]({% link _docs/adding-ruby-projects.md %})
- Deployed to [AWS](https://aws.amazon.com)
- Hosted on [GitHub](https://github.com), [GitHub Enterprise](https://github.com/enterprise), [Bitbucket](https://bitbucket.org/), and [GitLab](https://gitlab.com)

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

Once authorized, you can select your repo. Seed will look for the `serverless.yml` file in your project root.

If you are unable to find your repo, it might be because Seed doesn't have the permissions to access your repo. You can [read about how to fix this here]({% link _docs/cannot-find-my-repo.md %}).

![Auto-detect serverless.yml for new app](/assets/docs/index/auto-detect-serverless-yml-for-new-app.png)

If detected, you can select to add this service. And Seed will create your app with it.

![Confirm default service for new app](/assets/docs/index/confirm-default-service-for-new-app.png)

Alternatively, you can add a different service by picking a different path.

![Pick different default service for new app](/assets/docs/index/pick-different-default-service-for-new-app.png)

You can always add additional services later. Or continue (even if Seed is unable to detect a `serverless.yml`), by hitting **Do this later**.

![Continue without detecting service for new app](/assets/docs/index/continue-without-detecting-service-for-new-app.png)

If you've added an app before, you have the option of configuring your new app with the settings of an existing app. Hit the **Inherit Settings** tab.

![Switch to inherit settings tab for new app](/assets/docs/index/switch-to-inherit-settings-tab-for-new-app.png)

Here you can select one of your existing apps.

![Select existing app settings for new app](/assets/docs/index/select-existing-app-settings-for-new-app.png)

Seed will create your new app using the following from the selected app:

- Stages
- CI settings
- IAM settings
- Stage IAM settings
- Stage notification settings
- Stage environment variables

> A personal app can only inherit the settings from another personal app. And the same applies to organization apps.

This is useful when you are adding multiple apps and they all share similar settings. This way you won't have to configure all the settings for a new app by hand. Note that, you can still tweak the settings manually even if they have been inherited.

Next, let's look at how to create a an [AWS IAM Role]({% link _docs/adding-your-iam-credentials.md %}).
