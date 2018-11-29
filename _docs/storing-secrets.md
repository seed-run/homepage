---
layout: docs
title: Storing Secrets
---

At times your code needs to access sensitive information such as private keys, passwords, and access tokens. You should avoid storing these in your `serverless.yml`. Seed lets you store them as secret environment variables through the Seed console.

When you first create a Seed project, an encryption key is generated and stored in your [AWS KMS](https://aws.amazon.com/kms/) account. Seed uses this key to encrypt the secret value when you create a secret variable, and stores the encrypted value. And upon deployment, Seed decrypts the value and sets it as a Lambda environment variable.

> Seed encrypts your secrets using your AWS KMS keys

You can then access them in your Node.js Lambda functions using the `process.env` object.

To add a secret, select the stage you are trying to set it for.

![Select stage](/assets/docs/storing-secrets/select-stage.png)

And hit **Settings**.

![Stage Settings](/assets/docs/storing-secrets/stage-settings.png)

Select **Show Env Variables**.

![Show Env Variables](/assets/docs/storing-secrets/show-env-variables.png)

Enter the **Key** and **Value** for the new secret, and click **Add**.

![Create Secret Variable](/assets/docs/storing-secrets/create-secret-variable.png)

Note that the newly created secrets will take effect only after the next deployment to this stage. And these secrets will be available to all the services in your application.

Secret variables take precedence over the [other stage variables](% link _docs/configuring-stage-variables.md %}) defined in `serverless.yml`. If you were to define a secret variable, and the same variable is defined in the yaml file; the value defined in `serverless.yml` is overridden.

> Secrets take precedence over other environment variables

This is useful when you are developing on your local where your Lambda functions are not going to have access to the secrets from the Seed console.

> Secrets are available in your build process

For example, we just created a secret variable **DB_PASSWORD** for the **production** stage. The same variable is also defined in the `serverless.yml`.

``` yaml
service: service-name

provider:
  name: aws
  environment:
    DB_PASSWORD: '1234567890'
```

When invoking your function on any other environment other than production, the `process.env.DB_PASSWORD` returns the value defined in `serverless.yml`. And in the case of **production** it returns the secret value that you had set in the Seed console.

``` javascript
export function main(event, context, callback) {

  console.log(process.env.DB_PASSWORD);

  ...
}
```

Finally, you can access your secrets just as you would access any other environment variable in Lambda.
