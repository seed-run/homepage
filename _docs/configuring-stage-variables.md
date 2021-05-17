---
layout: docs
title: Configuring Stage Variables
---

Serverless Framework lets you define Lambda environment variables in `serverless.yml` that can be accessed in your Node.js Lambda functions using the `process.env` object. In Seed, you can set up stage specific variables easily by referring to the stage names in your Seed project.

Let's look at an example.

The following `serverless.yml` file defines the **MESSAGE** stage variable that takes on a stage specific value.

``` yaml
service: service-name

custom:
  myEnvironment:
    MESSAGE:
      prod: "This is production environment"
      dev: "This is development environment"

provider:
  name: aws
  environment:
    MESSAGE: ${self:custom.myEnvironment.MESSAGE.${opt:stage}}
```

Here the value `${opt:stage}` comes from the `--stage` option in the `serverless deploy` command. Internally, Seed deploys your stages using the `serverless deploy --stage SEED_STAGE_NAME` command. Where the `SEED_STAGE_NAME` in the name of the stage you set up in the Seed console. The stage name in your Seed console should map to the stage variables you add in your `serverless.yml`. You can read more about this in the [adding a stage]({% link _docs/adding-a-stage.md %}) chapter.

![Stages](/assets/docs/configuring-stage-variables/stages.png)

In the example above, we have the stage variables based on the `prod` and `dev` stages in our `serverless.yml` and we have the exact same stages in our Seed console.

> The stage name in your Seed console should map to your stage variables

This ensures that without any additional configuration the value of `process.env.MESSAGE` in our Lambda function will have the stage specific value that was set above.

``` javascript
export function main(event, context, callback) {

  // Should output
  // "This is production environment" in the prod stage
  // "This is development environment" in the dev stage
  console.log(process.env.MESSAGE);

  ...
}
```

Finally, it is strongly discouraged to store sensitive values (or secrets) in your `serverless.yml`. For more details on this refer to the chapter on [storing secrets]({% link _docs/storing-secrets.md %}).
