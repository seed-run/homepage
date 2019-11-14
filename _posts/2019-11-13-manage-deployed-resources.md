---
layout: post
title: Manage deployed resources
categories: news
author: jack
---

We are rolling out some changes to the Seed console to make it easier for you to manage your Serverless apps.

![New deployment info design](/assets/blog/manage-deployed-resources/new-deployment-info-design.png)

Once your app has been deployed with Seed, it'll pull up the following information:

- A complete list of **all the Lambda functions** that have been deployed. This includes the API path that the Lambda function responds to.
- The **API Gateway endpoint** for the service (and the custom domain, if it has been configured).
- The **CloudFormation stack outputs** with an easy way to copy the values.
- And a complete list of all the **other resources** that have been deployed.

![Copy stack outputs in deployment info](/assets/blog/manage-deployed-resources/copy-stack-outputs-in-deployment-info.png)

You can also click through to view the Lambda logs and Access logs for your API Gateway endpoints.

The new design also gives you an overview of all your services, making it easier to manage all your resources in your Serverless app.
