---
layout: build-errors
title: You are not currently logged in
image: /assets/social-cards/common-errors.png
description: You are not currently logged in
---

#### Error Message

You might see one of the following error messages:

> You are not currently logged in. To log in, use: $ serverless login

> Please log in by running "serverless login"


#### Problem

Serverless Framework tries to log you into your Serverless Pro account when you have a Serverless organization specified in your `serverless.yml`:

``` yml
org: acme
service: notes

...
```

If the `org` is specified but you have not logged in to Serverless, you will get this error.

#### Solution

If you are not deploying a [Serverless Component](https://www.serverless.com/components/), and want to skip the login step, you can simply comment out the `org` definition.

``` yml
# org: acme
service: notes
```

However, if you are deploying a Serverless Component, you'll need to login using the `$ serverless login` command.

**Deploying Through Seed:**

If you are deploying through Seed, you'll need to setup a Serverless Access Key. Follow our docs on getting setup — [Integrating with Serverless Pro]({% link _docs/integrating-with-serverless-pro.md %}).
