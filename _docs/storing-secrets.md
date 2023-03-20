---
layout: docs
title: Storing Secrets
---

In general it's recommended that you use [AWS SSM](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-parameter-store.html) to store secrets for your Serverless app. However, there are times when you need some secrets to be involved in the build process. You should avoid storing these in your `serverless.yml`. Seed lets you store them as secret environment variables through the Seed console.

Seed internally encrypts them using [AWS KMS](https://aws.amazon.com/kms/) and stores them. They are then decrypted and made available in the build process.

Additionally for Serverless Framework applications, Seed sets them as Lambda environment variables. You can then access them in your Node.js Lambda functions using the `process.env` object. To opt out of this behavior, [set `sls_set_secret_envs` to false in the build spec](./adding-a-build-spec.md#disabling-setting-seed-secrets-as-lambda-environment-varaibles-for-serverless-framework).

To add a secret, head over to your app settings.

![App Settings](/assets/docs/storing-secrets/app-settings.png)

Select the stage you are trying to set it for.

![Stage Settings](/assets/docs/storing-secrets/stage-settings.png)

Select **Show Env Variables**.

![Show Env Variables](/assets/docs/storing-secrets/show-env-variables.png)

Enter the **Key** and **Value** for the new secret, and click **Add**.

![Create Secret Variable](/assets/docs/storing-secrets/create-secret-variable.png)

Note that the newly created secrets will take effect only after the next deployment to this stage. And these secrets will be available to all the services in your application.

### Serverless Framework

Secret variables take precedence over the [other stage variables](% link \_docs/configuring-stage-variables.md %}) defined in `serverless.yml`. If you were to define a secret variable, and the same variable is defined in the yaml file; the value defined in `serverless.yml` is overridden.

> Secrets take precedence over other environment variables

This is useful when you are developing on your local where your Lambda functions are not going to have access to the secrets from the Seed console.

> Secrets are available in your build process

For example, we just created a secret variable **DB_PASSWORD** for the **production** stage. The same variable is also defined in the `serverless.yml`.

```yaml
service: service-name

provider:
  name: aws
  environment:
    DB_PASSWORD: "1234567890"
```

When invoking your function on any other environment other than production, the `process.env.DB_PASSWORD` returns the value defined in `serverless.yml`. And in the case of **production** it returns the secret value that you had set in the Seed console.

```javascript
export function main(event, context, callback) {

  console.log(process.env.DB_PASSWORD);

  ...
}
```

Finally, you can access your secrets just as you would access any other environment variable in Lambda.

### SST

For SST apps, you can grab the secrets from the build environment and set it in your Lambda functions. So for example, if you wanted to set a secret variable for all the functions in your app, you can use the [`addDefaultFunctionEnv`](https://docs.serverless-stack.com/constructs/App#adddefaultfunctionenv) method.

```javascript
app.addDefaultFunctionEnv({
  DB_PASSWORD: process.env.DB_PASSWORD,
});
```

And now you can use `process.env.DB_PASSWORD` in your Lambda functions.
