---
layout: docs
title: Enabling GitLab Self-Managed
---

Seed can easily connect to your GitLab Self-Managed account. This allows you to add a fully-managed CI/CD pipeline for your Serverless apps hosted on GitLab Self-Managed.

Note that, GitLab Self-Managed support is available as a part of our **Enterprise** plan. You can read more about [our pricing plans here]({% link pricing.html %}).

In this chapter, we'll look at how to enable GitLab Self-Managed for your organization on Seed.


### Prerequisites

Start by creating an organization on Seed by following the steps in [this chapter]({% link _docs/creating-an-organization.md %}).


### Add a GitLab OAuth App

Next we'll create an OAuth app for Seed on GitLab.

1. Head over to your GitLab Self-Managed Console.

2. Click on your avatar on the top right and hit **Settings**.

   ![Click GitLab Self-Managed settings](/assets/docs/enabling-gitlab-self-managed/click-gitlab-self-managed-settings.png)

3. Click on **Applications**.

   ![Click on Applications](/assets/docs/enabling-gitlab-self-managed/click-on-applications.png)

4. Fill out the form with the following.

   Name: Seed  
   Redirect URI: `https://console.seed.run/new/callback/gitlab-enterprise`  

   Uncheck **Confidential**

   Check `api`, `read_user` and `read_repository` under **Scopes**.

   ![Fill out new Application form](/assets/docs/enabling-gitlab-self-managed/fill-out-new-application-form.png)

5. Scroll down and hit **Save application**.

   ![Save Application](/assets/docs/enabling-gitlab-self-managed/save-new-application.png)

6. Copy the **Application ID** and the **Secret**.

   ![Copy the Application ID and Secret](/assets/docs/enabling-gitlab-self-managed/copy-the-application-id-and-the-secret.png)

### Enable GitLab Self-Managed on Seed

Now head over to your **organization settings** on Seed. Here you'll be able to put in your:

- **Organization domain** (ex: gitlab.my-corp-domain.com)
- **Application ID** & **Secret** (from above)

![Enabled GitLab Self-Managed on Seed](/assets/docs/enabling-gitlab-self-managed/enable-gitlab-self-managed-on-seed.png)

Note that, you'll need to be on the Enterprise plan to be able to enable GitLab Self-Managed on Seed.
