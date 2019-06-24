---
layout: build-errors
title: IamRoleLambdaExecution - Resource must be in ARN format or
image: /assets/social-cards/common-errors.png
description: IamRoleLambdaExecution - Resource xxxx-xxxx-xxxx must be in ARN format or "*".
---

#### Error Message

> IamRoleLambdaExecution - Resource xxxx-xxxx-xxxx must be in ARN format or "*".


#### Problem

The `Resource` attribute for an IAM policy (ie. the one you define in the IAM role statement block of your `serverless.yml`) should be one of the following:

- an ARN value of a resource, which starts with `arn:`; or
- an array of ARN values; or
- `*` to match all resources

#### Solution

A common mistake here is using the resource name instead of the ARN. So ensure that you are not using the name of the resource (for example, `users-table`), but rather the ARN of the resource (for ex, `arn:aws:dynamodb:us-east-1:xxxxxxxxxxxx:table/users-table`).
