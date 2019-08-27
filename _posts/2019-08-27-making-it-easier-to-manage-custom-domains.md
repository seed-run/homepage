---
layout: post
title: Making it easier to manage custom domains
image: assets/social-cards/custom-domains.png
categories: news
author: jay
---

We recently revamped the part of [Seed](/) that helps you manage the custom domains for your [Serverless Framework](https://serverless.com) apps.

![Managing Serverless Custom Domain in Seed](/assets/blog/making-it-easier-to-manage-custom-domains/managing-serverless-custom-domain-in-seed.png)

Managing your custom domains in Seed is now a lot more easier and far more reliable. Here is a quick rundown of the improvements:

1. You can manage all your custom domains **centrally in your app settings**.
2. Seed will use the [stage specific IAM credentials]({% link _docs/iam-credentials-per-stage.md %}) to get the list of available domains.
3. API endpoints of **all kinds are now supported**; WebSocket, Rest API, Regional, or Edge-optimized.
4. The various steps in the process of setting the custom domain are displayed clearly.
5. You'll be **notified via email** once the custom domain has been configured.
6. And finally, you'll receive some helpful error messages in case the custom domain could not be configured.

<div style="text-align: center;">
  <img src="/assets/blog/making-it-easier-to-manage-custom-domains/custom-domain-configured-notification.png" alt="Custom domain configured notification" width="600" />
</div>

We've also updated our docs with the above. You can read about it in detail in the [Configuring Custom Domains]({% link _docs/configuring-custom-domains.md %}) chapter.

We hope this update makes it easier for you to setup and manage the custom domain endpoints for your Serverless Framework apps!
