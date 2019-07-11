---
layout: docs
title: Integrating with Serverless Enterprise
---

If you are using the [Serverless Enterprise Plugin](https://github.com/serverless/enterprise-plugin), there are a couple of steps you need to follow to get your app to work with Seed.

1. Create an access key in the Serverless Enterprise Dashboard

   ![Create an access key in the Serverless Enterprise Dashboard](/assets/docs/integrating-with-serverless-enterprise/create-an-access-key-in-the-serverless-enterprise-dashboard.png)

2. Add the access key as an environment variable on Seed. Make sure to name your variable `SERVERLESS_ACCESS_KEY`. You'll need to do this for all the stages you are deploying to.  If you need some help, here is how to [add an environment variable in Seed]({% link _docs/storing-secrets.md %}).

   ![Add Serverless Access Key as Seed environment variable](/assets/docs/integrating-with-serverless-enterprise/add-serverless-access-key-as-seed-environment-variable.png)



That's it! Try deploying your app again and your Serverless Enterprise plugin should work correctly.
