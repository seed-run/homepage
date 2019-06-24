---
layout: build-errors
title: Export with name is already exported by stack
image: /assets/social-cards/common-errors.png
description: Export with name dev-ApiGatewayRestApiRootResourceId is already exported by stack xxxx-xxxx-xxxx-dev.
---

#### Error Message

> Export with name dev-ApiGatewayRestApiRootResourceId is already exported by stack xxxx-xxxx-xxxx-dev.


#### Problem

CloudFormation export key names are unique per region in your AWS account. Your CloudFormation stack is exporting a value with the key name that is already being exported by another stack.

#### Solution

Change the export key name in the current stack or the one that was previously exporting it.

The error message should tell you which stack is exporting it. Or you can go to your CloudFormation console and view a list of all currently exported values.

```
https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/exports
```

Make sure to replace `us-east-1` with the region your region in the above URL.
