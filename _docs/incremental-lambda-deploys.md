---
layout: docs
title: Incremental Lambda Deploys
---

To speed up Serverless deployments, Seed incrementally deploys the Lambda functions in your service. It does this by checking if the CloudFormation template or Serverless config has been changed. If it hasn't, then it'll look at the individual Lambda functions in the service and deploy only the ones that have been updated. It'll deploy the **Lambda functions concurrently and directly**, without doing a CloudFormation update.

Updating individual Lambda functions directly is a lot faster than having CloudFormation deploy the entire stack. To do this, Seed maintains an internal state of the deployed service using the [**Serverless Seed plugin**](https://github.com/seed-run/serverless-seed).

Incremental Lambda Deploys is currently in beta.

### Enabling Incremental Deploys

To enable incremental deployments for your Lambda functions, first install the [`serverless-seed` plugin](https://github.com/seed-run/serverless-seed):

``` bash
$ npm install --save-dev serverless-seed
```

Then add it to your `serverless.yml`.

``` yml
plugins:
  - serverless-seed
```

And enable Incremental Lambda Deploys.

``` yml
custom:
  seed:
    incremental:
      enabled: true
```

And that's it.

### How it works

Once enabled, the `serverless-seed` plugin generates the state of the service when it's deployed. This contains a hash of the CloudFormation template and Serverless config of the service. It also includes a list of all the Lambda functions in the service and their packages. Seed stores this information internally.

Now when you push a change, Seed will:

1. Generate a new state file using the `serverless-seed` plugin.
2. Check if the CloudFormation template or Serverless config has been updated.
3. If they have, then it'll proceed with the deployment as is.
4. If they haven't been updated, then it'll do an Incremental Deploy.
5. It'll check which of the Lambda functions have been updated.
6. And update them directly without doing a full CloudFormation deploy.
7. Finally, it'll save the new state of the service.

Incremental Lambda Deploys are automatically disabled for a deployment if:

- The previous build had failed
- The [_Force Deploy_ option]({% link _docs/manually-deploying.md %}#force-deploys) was used
- The [environment variables]({% link _docs/storing-secrets.md %}) were updated
- There are no Lambda functions in the service
- The Lambda Layers in the service were updated
- Or, there was a problem generating the service state

### Disabling for production

It is recommended that you use Incremental Lambda Deploys in your development stages and do a full deployment in your prod or staging stages. To configure this, you can selectively disable it for certain stages.

In your `serverless.yml`, update the `serverless-seed` config to.

``` yml
custom:
  seed:
    incremental:
      enabled: true
      disabledFor:
        - prod
        - staging
```

The `disabledFor` option takes a list of stage names that you want to disable incremental Lambda deployments for.
