---
layout: docs
title: Integrating with Serverless Pro
redirect_from: /docs/integrating-with-serverless-enterprise.html
---


[Serverless Pro](https://www.serverless.com/pro/) offers some similar features to Seed, like deployments and viewing logs and metrics. However, most of our users just use Seed. But if you'd like to deploy using Seed while viewing logs or metrics on Serverless Pro, you'll need to follow a couple of quick steps.

1. Create an access key in the Serverless Pro Dashboard

   ![Create an access key in the Serverless Enterprise Dashboard](/assets/docs/integrating-with-serverless-pro/create-an-access-key-in-the-serverless-enterprise-dashboard.png)

2. Add the access key as an environment variable on Seed. Make sure to name your variable `SERVERLESS_ACCESS_KEY`. You'll need to do this for all the stages you are deploying to.  If you need some help, here is how to [add an environment variable in Seed]({% link _docs/storing-secrets.md %}).

   ![Add Serverless Access Key as Seed environment variable](/assets/docs/integrating-with-serverless-pro/add-serverless-access-key-as-seed-environment-variable.png)

That's it! Try again and your app should deploy correctly.
