---
layout: post
title: Setting Custom Domains
categories: news
author: jay
---

Seed can now help you configure custom domains for your API Gateway endpoints with just a couple of clicks. Simply pick the domain, sub domain, and base path. And Seed will configure the SSL certificates and IAM permissions necessary for it.

![Configure Custom Domain parts Screenshot](/assets/blog/setting-custom-domains/update-custom-domain-parts.png)

Previously, the process of setting up a custom domain for your Serverless projects on [AWS was fairly complicated](https://docs.aws.amazon.com/apigateway/latest/developerguide/how-to-custom-domains.html). The [serverless-domain-manager](https://github.com/amplify-education/serverless-domain-manager) plugin has [simplified this a bit](https://serverless.com/blog/serverless-api-gateway-domain/). But this process can still be error prone while making it hard to collaborate with the rest of your team. Seed gives you a simple and robust way to manage this so that it fits well with your team's deployment workflow.

Just head over to the deployment settings for the stage you are trying to configure. You can [read more about configuring custom domains in our docs]({% link _docs/configuring-custom-domains.md %}).
