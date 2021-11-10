---
layout: docs
title: Using Serverless Plugins
---

Seed supports most of the common [Serverless Framework plugins](https://github.com/serverless/plugins) out of the box. The exception, would be plugins that are not related to the build or deployment process of the app. If you are having problems getting a specific plugin to work, <a href="mailto:{{ site.email }}">feel free to contact us</a>.

Below are a list of plugins that need some additional configuration to work with Seed.


### serverless-domain-manager

The [serverless-domain-manager](https://github.com/amplify-education/serverless-domain-manager) is an alternative to [configuring custom domains with Seed]({% link _docs/configuring-custom-domains.md %}). The major difference is that Seed will automatically create the SSL certificates necessary for your custom domain.

However, if you are already using the serverless-domain-manager plugin, you need to configure it using the following options:

1. Set it up locally

   Run the `serverless create_domain --stage $STAGE_NAME` command locally where `$STAGE_NAME` is the name of the stage that needs to be configured.

2. Or configure it using the `seed.yml`

   Add the following to your [Seed build spec]({% link _docs/adding-a-build-spec.md %}). Or if you don't have a build spec, create a `seed.yml` file in your project root with the following:

   ``` yml
   before_build:
     - serverless create_domain --stage $SEED_STAGE_NAME
   ```

   Here `$SEED_STAGE_NAME` is an environment variable that is set automatically as a part of the build process.
 
   Note that this build hook will be run in your project root for ALL your services. So if you want to run it for a specific service you'll need something like this: 
 
   ``` yml
   before_build:
     - if [ $SEED_SERVICE_NAME = "my-service" ]; then cd my-service/ && serverless create_domain --stage $SEED_STAGE_NAME; fi
   ```
 
   Where `my-service/` is the path to the service with the custom domain configured.


### serverless-plugin-canary-deployments

The [serverless-plugin-canary-deployments](https://github.com/davidgf/serverless-plugin-canary-deployments) plugin is used to implement canary deployments of Lambda functions using AWS CodeDeploy.

It works with Seed without any changes. However, depending on the traffic shifting configuration that is used, your builds might time out. For example, `Linear10PercentEvery10Minutes` strategy will take over an hour to completely deploy your app. Builds in Seed (on the free tier) have roughly a 20min timeout. You'll need to upgrade to [one of our paid plans]({% link pricing.html %}) and we'll raise the timeout to fix this.
