---
layout: docs
title: Getting Started with Seed
description: Documentation for using Seed to build and deploy Serverless apps
---

Seed is a fully-configured code pipeline for building and deploying Serverless apps on AWS. Simply add your Git repository and IAM credentials and your entire team can `git push` to deploy updates to your Serverless app.

Seed currently supports the following:

- [Serverless Framework](https://serverless.com/framework/) projects
- Built with [Node.js](https://nodejs.org/en/), [Python](https://www.python.org), [.NET Core](https://github.com/dotnet/core), [Go](https://golang.org/), and [Ruby](https://www.ruby-lang.org/en/)
- Deployed to [AWS](https://aws.amazon.com)
- Hosted on [GitHub](https://github.com), [Bitbucket](https://bitbucket.org/), and [GitLab](https://gitlab.com)

Support for other platforms and repositories are coming soon. [Send us an email](mailto: {{ site.email }}) to let us know what you would like us to support next.

### Prerequisites

Seed needs very little configuration on your part and there is no CLI to install. But to add your project you need to:

1. Add your project repository with your Git provider
2. Create an IAM Role for your AWS account

![Create a new app](/assets/docs/index/create-a-new-app.png)

Once you select your repo, Seed will look for the `serverless.yml` file in your project root.

![Auto-detect serverless.yml for new app](/assets/docs/index/auto-detect-serverless-yml-for-new-app.png)

If detected, you can select to add this service. And Seed will create your app with it.

![Confirm default service for new app](/assets/docs/index/confirm-default-service-for-new-app.png)

Alternatively, you can add a different service by picking a different path.

![Pick different default service for new app](/assets/docs/index/pick-different-default-service-for-new-app.png)

You can always add additional services later. Or continue even if Seed is unable to detect a `serverless.yml`.

![Continue without detecting service for new app](/assets/docs/index/continue-without-detecting-service-for-new-app.png)

Next, let's look at how to create a an [AWS IAM Role]({% link _docs/adding-your-iam-credentials.md %}).
