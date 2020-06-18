---
layout: common-errors
title: Code storage limit exceeded
image: /assets/social-cards/common-errors.png
description: Code storage limit exceeded.
---

#### Error Message

> Code storage limit exceeded.


#### Problem

AWS has a limit of 75GB on the size of all the deployment packages that can be uploaded per region. This includes all of your Lambda functions and all their historical versions combined in a given region.

The error could happen if you have a large number of Lambda functions that have been deployed many times. Each deployment creates a version and this can add up over time.

You can read more about [the limits here](https://docs.aws.amazon.com/lambda/latest/dg/limits.html).


#### Solution

You have two options:

1. If you do not need to version your Lambda functions, you can turn off Lambda versioning by setting it in your `serverless.yml`.

   ``` yml
   ...
   
   provider:
     name: aws
     versionFunctions: false
   
   ...
   ```

2. Alternatively, you can manually remove older Lambda versions. You can use the [**serverless-prune-plugin**](https://github.com/claygregory/serverless-prune-plugin) to automate the process for you. The plugin can be used to do a one-time clean up, or can be configured in your serverless.yml to auto prune older Lambda versions after each deployment.
