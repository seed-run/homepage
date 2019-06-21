---
layout: build-errors
title: Service files not changed. Skipping deployment.
image: /assets/social-cards/common-errors.png
description: Service files not changed. Skipping deployment...
---

#### Error Message

> Service files not changed. Skipping deployment...


#### Problem

On each deployment, Serverless Framework checks if your Lambda code and config have changed by computing the SHA checksum and comparing it to the previous deployment. If unchanged, Serverless skips the deployment.

This can be undesirable if your previous deployment failed due to an external factor that has nothing to do with your code.


#### Solution

Serverless Framework has an option to skip this check and deploy anyway. Use the `--force` flag when you run `serverless deploy`.

```
$ serverless deploy --stage dev --force
```
