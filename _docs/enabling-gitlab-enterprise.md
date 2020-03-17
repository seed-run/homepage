---
layout: docs
title: Enabling GitLab Enterprise
---

Seed can easily connect to your GitLab Enterprise account. This allows you to add a fully-managed CI/CD pipeline for your Serverless apps hosted on GitLab Enterprise.

Note that, GitLab Enterprise support is available as a part of our **Enterprise** plan. You can read more about [our pricing plans here]({% link pricing.html %}).

In this chapter, we'll look at how to enable GitLab Enterprise for your organization on Seed.


### Prerequisites

Start by creating an organization on Seed by following the steps in [this chapter]({% link _docs/creating-an-organization.md %}).


### Add a GitLab OAuth App

Next we'll create an OAuth app for Seed on GitLab.

1. Head over to your GitLab Enterprise Console.

2. Click on your avatar on the top right and hit **Settings**.

   ![Click GitLab Enterprise settings](/assets/docs/enabling-gitlab-enterprise/click-gitlab-enterprise-settings.png)

3. Click on **Applications**.

   ![Click on Applications](/assets/docs/enabling-gitlab-enterprise/click-on-applications.png)

4. Fill out the form with the following.

   Name: Seed  
   Redirect URI: `https://console.seed.run/new/callback/gitlab-enterprise`  

   Uncheck **Confidential**

   Check `api`, `read_user` and `read_repository` under **Scopes**.

   ![Fill out new Application form](/assets/docs/enabling-gitlab-enterprise/fill-out-new-application-form.png)

5. Scroll down and hit **Save application**.

   ![Save Application](/assets/docs/enabling-gitlab-enterprise/save-new-application.png)

6. Copy the **Application ID** and the **Secret**.

   ![Copy the Application ID and Secret](/assets/docs/enabling-gitlab-enterprise/copy-the-application-id-and-the-secret.png)

### Send us your details

Finally, send an email to [{{ site.email }}](mailto:{{ site.email }}) with:

- Your Organization name
- The Organization domain (ex: gitlab.my-corp-domain.com)
- Application ID & Secret (from above)

And we'll have GitLab Enterprise enabled for your organization on Seed!

