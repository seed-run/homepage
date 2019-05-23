---
layout: docs
title: Enabling GitHub Enterprise
---

Seed can easily connect to your GitHub Enterprise account. This allows you to add a fully-managed CI/CD pipeline for your Serverless apps hosted on GitHub Enterprise.

Note that, GitHub Enterprise support is available as a part of our **Enterprise** plan. You can read more about [our pricing plans here]({% link pricing.html %}).

In this chapter, we'll look at how to enable GitHub Enterprise for your organization on Seed.


### Prerequisites

Start by creating an organization on Seed by following the steps in [this chapter]({% link _docs/creating-an-organization.md %}).


### Add a GitHub OAuth App

Next we'll create an OAuth app for Seed on GitHub.

1. Head over to your GitHub Enterprise Console.

2. Click on your avatar on the top right and hit **Settings**.

   ![Click GitHub Enterprise settings](/assets/docs/enabling-github-enterprise/click-github-enterprise-settings.png)

3. Click on the organization under Organization settings.

   ![Click on organization under Organization settings](/assets/docs/enabling-github-enterprise/click-on-organization-under-organization-settings.png)

4. Click on **OAuth Apps**.

   ![Click on OAuth Apps](/assets/docs/enabling-github-enterprise/click-on-oauth-apps.png)

5. Click on **New OAuth App**.

   ![Click on New OAuth App](/assets/docs/enabling-github-enterprise/click-on-new-oauth-app.png)

6. Fill out the form with the following and hit **Register application**.

   Application name: Seed  
   Homepage URL: `https://seed.run`  
   Application description: A fully-managed CI/CD pipeline for Serverless Framework.  
   Authorization callback URL: `https://console.seed.run/new/callback/github-enterprise`  

   ![Fill out new OAuth App form](/assets/docs/enabling-github-enterprise/fill-out-new-oauth-app-form.png)

7. (Optional) Add the Seed logo and colors.

   Logo image: `https://anomaly.s3.amazonaws.com/Seed/github-oauth-icon.png`    
   Badge background color: `#53437D`  

8. Copy the **Client ID** and the **Client Secret**.

   ![Copy the Client ID and Client Secret](/assets/docs/enabling-github-enterprise/copy-the-client-id-and-the-client-secret.png)

### Send us your details

Finally, send an email to [{{ site.email }}](mailto:{{ site.email }}) with:

- Your Organization name
- The Organization domain (ex: ghe.my-corp-domain.com)
- Client ID & Client Secret (from above)

And we'll have GitHub Enterprise enabled for your organization on Seed!
