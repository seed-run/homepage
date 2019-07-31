---
layout: post
title: Testing your Serverless app
image: assets/social-cards/testing-serverless-apps.png
description: In this post we look at the different types of testing you might do for your Serverless app. Use the serverless invoke local command on local, unit tests with mocked AWS services as a part of your deployment process, and take advantage of the Serverless pay per use model to use multiple test environments for your integration tests.
categories: tips
author: jack
---

In this post we are going to look at some general strategies on how to test Serverless apps. We'll look at what is involved from a testing perspective while developing, before deploying, and after deploying your app.

Let's start by looking at how to test your app while you are actively developing it.

### Local tests during development

While working on your Lambda functions, you want to be able to run them without having to push them to AWS every single time. To do this simply run the `serverless invoke local` command. For example, to test a Lambda function called `create` you can run the following:

``` bash
$ serverless invoke local --function create
```

Where the `--function` option allows you to specify the name of the Lambda function. 

If your Lambda function expects some event data, you can pass this by using the `--path` option. 

``` bash
$ serverless invoke local --function create --path mocks/create-event.json
```

Where `mocks/create-event.json` might look something like this:

``` json
{
  "body": "{\"content\":\"hello world\",\"attachment\":\"hello.jpg\"}",
  "requestContext": {
    "identity": {
      "cognitoIdentityId": "USER-SUB-1234"
    }
  }
}
```

Finally, you'll need to be careful if your Lambda function is internally invoking some AWS services. It'll use your default AWS profile. If you want to use a different AWS profile, you can specify it using the `AWS_PROFILE` option.

``` bash
$ AWS_PROFILE=myProfile serverless invoke local --function create --path mocks/create-event.json
```

Where `myProfile` is specified in my `~/aws/credentials`. You can read more about [using multiple AWS profiles here](https://serverless-stack.com/chapters/configure-multiple-aws-profiles.html).

If you are working on an API endpoint and you'd like to test the endpoint locally you can look into using the [serverless-offline](https://www.github.com/dherault/serverless-offline) plugin.

### Unit testing Lambda functions

Now that you are developing your functions locally, you might want to add some unit tests to them. For Node.js you can use [Mocha](https://mochajs.org), [Jest](https://jestjs.io), or any of the other options. You'll need to install the packages and set up the config for them.

We have a great plugin called [serverless-bundle](https://github.com/AnomalyInnovations/serverless-bundle) that can help you with this. This plugin will let you write tests using modern ES syntax without any additional config. Simply install it using:

``` bash
$ npm install --save-dev serverless-bundle
```

Then add it to your `serverless.yml`.

``` yml
plugins:
  - serverless-bundle
```

And add the following to your `package.json`.

``` json
"scripts": {
  "test": "serverless-bundle test"
}
```

Now you can run your Jest unit tests using:

``` bash
$ npm test
```

Note that, if your Lambda functions are invoking other AWS services, you might want to mock them for your unit tests. The [AWS SDK Mock](https://github.com/dwyl/aws-sdk-mock) package is a good option for this.

### Integration tests

Once your Serverless app has been deployed, you might want to run a test suite to ensure that your deployment has been successful. This can include integration tests, end-to-end tests, or user acceptance tests. For API backends, tests are usually run against the API endpoint that you've generated. This process isn't very different for Serverless apps but here are a couple of pointers.

- Serverless applications usually involve multiple AWS services in their stack. To ensure the AWS services' behavior, you should not mock them in these tests.
- Also, most Serverless services (Lambda, API Gateway, DynamoDB, etc.) are pay per use. This means that it is both easy and cost-effective to replicate a stack at scale.
- Your test environments should mirror production as closely as possible.
- The cost-effective nature of Serverless services allows you to setup multiple test environments to run your test suites in parallel. This is especially useful because integration tests can take a long time to run.
- For databases, DynamoDB has a great backup snapshot feature. Allowing you to create multiple test environments with the exact database state you want. Note that, this only works for environments created in the same AWS account.

### UI Tests

Just one final word on user interface testing. There is nothing specific for Serverless apps here. Tools like [Selenium](https://www.seleniumhq.org) and [Cypress](https://www.cypress.io) still work as expected.


#### Summary

And there you have it! This post should give you a good idea of the different types of testing you might do for your Serverless app. Use the `serverless invoke local` command on local, unit tests with mocked AWS services as a part of your deployment process, and take advantage of the Serverless pay per use model to use multiple test environments for your integration tests.
