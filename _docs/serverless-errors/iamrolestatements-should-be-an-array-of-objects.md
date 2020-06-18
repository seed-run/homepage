---
layout: common-errors
title: iamRoleStatements should be an array of objects
image: /assets/social-cards/common-errors.png
description: "iamRoleStatements should be an array of objects, where each object has Effect, Action, Resource fields. Specifically, statement 0 is missing the following properties: Resource"
---

#### Error Message

> iamRoleStatements should be an array of objects, where each object has Effect, Action, Resource fields. Specifically, statement 0 is missing the following properties: Resource


#### Problem

An IAM role statement block in your `serverless.yml` should have `Effect`, `Action` and `Resource`. Serverless Framework is not able to parse one or more of these fields.


#### Solution

Ensure that the `Effect`, `Action`, and `Resource` fields are specified. If they are there, check the formatting and indention of each line. It should look something like this:

``` yml
...

provider:
  iamRoleStatements:
    - Effect: 'Allow'
      Action:
        - 's3:ListBucket'
      Resource: '*'

...
```
