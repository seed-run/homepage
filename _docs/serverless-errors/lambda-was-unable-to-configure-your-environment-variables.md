---
layout: common-errors
title: Lambda was unable to configure your environment variables
image: /assets/social-cards/common-errors.png
description: "Lambda was unable to configure your environment variables because the environment variables you have provided contains reserved keys that are currently not supported for modification. Reserved keys used in this request: AWS_REGION, AWS_ACCESS_KEY"
---

#### Error Message

> Lambda was unable to configure your environment variables because the environment variables you have provided contains reserved keys that are currently not supported for modification. Reserved keys used in this request: AWS_REGION, AWS_ACCESS_KEY


#### Problem

Lambda functions come with a set of default environment variables. These environment variable names are reserved, and users will not be able to overwrite them.

According to the above error message, you are trying to assign values to the reserved `AWS_REGION` and `AWS_ACCESS_KEY` variable in your `serverless.yml`.

#### Solution

Rename the environment variable in your `serverless.yml`.

Here is a list of all [reserved environment variable names](https://docs.aws.amazon.com/lambda/latest/dg/lambda-environment-variables.html).
