---
layout: page
title: Docs
description: Documentation for using Seed to build and deploy Serverless apps
---

Seed is a fully-configured code pipeline for building and deploying Serverless apps on AWS. Simply add your GitHub repository and IAM credentials and your entire team can `git push` to deploy updates to your Serverless app. Here are a few things that can help you get started.


- Adding a new project
  - [Creating a GitHub Personal Access Token](#creating-a-github-personal-access-token)
  - [Adding your IAM Credentials](#adding-your-iam-credentials)
- Configuring your project
  - Adding stage variables
  - Storing secrets

<br />

# Creating a GitHub Personal Access Token

[Seed](/) uses your GitHub Personal Access Token to access your project repository. Use the following instructions from GitHub to create your Personal Access Token.

&rarr; [`Creating a personal access token`](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)

On **Step 6** while selecting the scopes for the token, make sure to select the **repo** and **admin:repo_hook** options as shown below.

![Select GitHub Personal Access Token Scopes Screenshot](/assets/docs/select-github-personal-access-token-scopes.png)

Seed needs these to access your repository and to add a Webhook to keep track of commits to your repository.

<br />

# Adding your IAM Credentials

[Seed](/) needs your AWS IAM credentials to deploy your project on your behalf to your AWS account. Follow these steps to generate your credentials.

Log in to your [AWS Console](https://console.aws.amazon.com) and select IAM from the list of services.

![Select IAM Service Screenshot](/assets/docs/iam/select-iam-service.png)

Select **Users**.

![Select IAM Users Screenshot](/assets/docs/iam/select-iam-users.png)

Select **Add User**.

![Add IAM User Screenshot](/assets/docs/iam/add-iam-user.png)

Enter a **User name** and check **Programmatic access**, then select **Next: Permissions**.

This account will be used by Seed. It will be connecting to the AWS API directly and will not be using the Management Console.

![Fill in IAM User Info Screenshot](/assets/docs/iam/fill-in-iam-user-info.png)

Select **Attach existing policies directly**.

![Add IAM User Policy Screenshot](/assets/docs/iam/add-iam-user-policy.png)

Search for **AdministratorAccess** and select the policy, then select **Next: Review**.

You can provide a more finely grained policy here based on your requirements. We'll be adding more documentation on this soon.

![Added Admin Policy Screenshot](/assets/docs/iam/added-admin-policy.png)

Select **Create user**.

![Review IAM User Screenshot](/assets/docs/iam/review-iam-user.png)

Select **Show** to reveal **Secret access key**.

![Added IAM User Screenshot](/assets/docs/iam/added-iam-user.png)

Take a note of the **Access key ID** and **Secret access key**.

![IAM User Credentials Screenshot](/assets/docs/iam/iam-user-credentials.png)

Use these as the **IAM Access Key** and the **IAM Secret Key** when you configure your project.

<br />


If you have any questions about the following or would like to see more details on a specific topic, please send us an email - [{{ site.email}}](mailto:{{ site.email }})
