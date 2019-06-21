---
layout: build-errors
title: The security token included in the request is invalid
image: /assets/social-cards/common-errors.png
description: The security token included in the request is invalid
---

#### Error Message

> The security token included in the request is invalid


#### Problem

This happens when the AWS credentials used for your Serverless command are invalid. Or if they have not been configured on your machine.


#### Solution

Double-check your credentials. Or you can create a new pair of credentials. You can follow the chapter on [creating and IAM user](https://serverless-stack.com/chapters/create-an-iam-user.html) over on Serverless Stack.

If you are trying to set up your local machine, run `aws configure` to set your credentials up.
