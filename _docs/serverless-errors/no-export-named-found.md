---
layout: common-errors
title: No export named found
image: /assets/social-cards/common-errors.png
description: xxx-xxxx-dev - No export named xx-xxx-us-east-1-dev-xxxxArn found.
---

#### Error Message

> xxx-xxxx-dev - No export named xx-xxx-us-east-1-dev-xxxxArn found.


#### Problem

CloudFormation is not able to find the exported value with the specified name.


#### Solution

Ensure the stack that is exporting the value has been successfully deployed, and that the exported value is listed in your CloudFormation console's exports page.

```
https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/exports
```

Make sure to replace `us-east-1` with your region in the above URL.

Also note that, CloudFormation exports are per region. Make sure that the stack that is exporting the value and the one importing it are in the same region.
