---
layout: docs
title: Integrating with Serverless Pro
redirect_from: /docs/integrating-with-serverless-enterprise.html
---

If you are deploying [Serverless Components](https://www.serverless.com/components/) or are looking to integrate with [Serverless Pro](https://www.serverless.com/pro/), there are a couple of quick steps you need to follow to get your app to work with Seed.

1. Create an access key in the Serverless Pro Dashboard

   ![Create an access key in the Serverless Enterprise Dashboard](/assets/docs/integrating-with-serverless-pro/create-an-access-key-in-the-serverless-enterprise-dashboard.png)

2. Add the access key as an environment variable on Seed. Make sure to name your variable `SERVERLESS_ACCESS_KEY`. You'll need to do this for all the stages you are deploying to.  If you need some help, here is how to [add an environment variable in Seed]({% link _docs/storing-secrets.md %}).

   ![Add Serverless Access Key as Seed environment variable](/assets/docs/integrating-with-serverless-pro/add-serverless-access-key-as-seed-environment-variable.png)

That's it! Try again and your app should deploy correctly.
