---
layout: post
title: How to manage secrets for your Serverless app?
image: /assets/social-cards/manage-serverless-secrets.png
author: frank
---

In this post we'll look at how to handle secrets for your [Serverless](https://serverless.com) app. Secrets or sensitive information that your app uses, should not be committed to source control. We'll look at the various ways to handle secrets in Serverless and their pros and cons.

Let's start with an example:

``` js
import Stripe from 'stripe';
const stripe = Stripe('YOUR_STRIPE_SECRET_KEY');
```

Where does the `YOUR_STRIPE_SECRET_KEY` come from?

### 1. Store in a local file

A common solution is to store this locally in something like a `env.yml` file. The key here is that the `env.yml` file is not committed to source control.

Let's look at how to store secrets locally and use them in your Serverless app:

1. Create a `env.yml` file with the following.

   ```
   stripeSecretKey: "sk_xxxx"
   ```

2. Add the `env.yml` in your `serverless.yml` as a Lambda environment variable.

   ``` yml
   provider:
     environment:
       stripeSecretKey: ${file(env.yml):stripeSecretKey}
   ```

3. Reference the secret in your Lambda function as a normal environment variable.

   ``` js
   const stripe = Stripe(process.env.stripeSecretKey);
   ```

4. Make sure the `env.yml` is not committed to Git by adding it to `.gitignore`.

**PROS**: Simple and does not rely on other AWS/third-party services.

**CONS**: The `env.yml` lives in your local environment and cannot be shared with your team.


### 2. Store in your CI/CD provider

Most CI/CD providers like [CircleCI](https://circleci.com), [Travis CI](https://travis-ci.org), and of course [Seed](/), let you store environment variables on their side. They are made available to you on deploy time, so you don't have to commit them in your code.

Here is how to store secrets in your CI/CD provider:

1. Add the secrets in your provider's console.

2. Since the secrets are available as build-time environment variables, reference them in your `serverless.yml` as Lambda environment variables.

   ``` yml
   provider:
     environment:
       stripeSecretKey: ${env:stripeSecretKey}
   ```

   Note that [environment variables in Seed]({% link _docs/storing-secrets.md %}) are directly available to your Lambda functions, so you don't need to do this step.

3. Finally, you can reference them in your code, just like you would for any other environment variable.

   ``` yml
   const stripe = Stripe(process.env.stripeSecretKey);
   ```

**PROS**: You can use this alongside a local `env.yml` file for both local and remote usage while keeping your Lambda code the same, ie. `process.env.stripeSecretKey`.

**CONS**: You have to manage your secrets through your CI/CD provider.


### 3. Use AWS Parameter Store

[AWS Systems Manager Parameter Store](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-parameter-store.html) (SSM) is an AWS service that lets you store configuration data and secrets as key-value pairs in a central place. The values can be stored as plain text or encrypted data. When stored as encrypted data, the value is encrypted on write using your KMS key, and decrypted on read.

Here is how you can use AWS Parameter Store to store your secrets:

1. Add the secrets in your [AWS Parameter Store Console](https://console.aws.amazon.com/systems-manager/parameters?region=us-east-1).

   ![Store secrets in AWS Parameter Store](/assets/blog/how-to-manage-secrets-for-your-serverless-app/store-secrets-in-aws-parameter-store.png)

2. Reference the value in your `serverless.yml` as a Lambda environment variable. Serverless Framework is able to fetch the value from your AWS Parameter Store account on deploy.

   ``` yml
   provider:
     environment:
       stripeSecretKey: ${ssm:stripeSecretKey}
   ```

3. Finally, you can reference it in your code just as before.

   ``` js
   const stripe = Stripe(process.env.stripeSecretKey);
   ```

**PROS**: You don't have to expose your secrets to 3rd party services. And again, you can use this along with a local `env.yml` file for both local and remote usage while keeping your Lambda code the same, ie. `process.env.stripeSecretKey`.

**CONS**: Since the secrets are decrypted and then set as Lambda environment variables on deploy, if you go to your Lambda console, you'll be able to see the secret values in plain text.
  

### 4. Store in AWS Parameter Store, and decrypt at runtime

To avoid exposing the secrets in plain text in your AWS Lambda Console, you can decrypt them at runtime instead. Here is how:

1. Add the secrets in your [AWS Parameter Store Console](https://console.aws.amazon.com/systems-manager/parameters?region=us-east-1) just as in the above steps.

2. Change your Lambda code to call the Parameter Store directly and decrypt the value at runtime.

   ``` js
   const aws = require('aws-sdk');
   const ssm = new aws.SSM();

   const stripeSecretKey = ssm.getParameter(
      { Name: 'stripeSecretKey', WithDecryption: true }
     ).promise();
   const stripe = Stripe(stripeSecretKey.Parameter.Value);
   ```

**PROS**: Your secrets are not exposed in plain text at any point.

**CONS**: Your Lambda code does get a bit more complicated, and there is an added latency since it needs to fetch the value from the store.

#### Summary

This should give you a really good idea of how to manage secrets for your Serverless app. Depending on the degree of sensitivity, you can use a combination of the approaches outlined above to store your secrets.
  
