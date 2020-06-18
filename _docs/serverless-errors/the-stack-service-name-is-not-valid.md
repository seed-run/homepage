---
layout: common-errors
title: The stack service name is not valid
image: /assets/social-cards/common-errors.png
description: The stack service name "xxxx-dev" is not valid. A service name should only contain alphanumeric (case sensitive) and hyphens. It should start with an alphabetic character and shouldn't exceed 128 characters.
---

#### Error Message

> The stack service name "xxxx-dev" is not valid. A service name should only contain alphanumeric (case sensitive) and hyphens. It should start with an alphabetic character and shouldn't exceed 128 characters.


#### Problem

CloudFormation stack names have the following restrictions:

- Only alphanumeric characters (case-sensitive) and hyphens
- Start with an alphabetic character
- Can't be longer than 128 characters

Serverless uses the service name to build the CloudFormation stack name. And so, service names inherit the above restrictions as well.


#### Solution

Change the service name to follow the above restrictions.

Alternatively, if you want to have control over the CloudFormation stack name, you can specify it directly in your `serverless.yml` provider section:

``` yml
...

provider:
  stackName: custom-stack-name

...
```

You can read more on this over on the [Serverless Framework docs](https://serverless.com/framework/docs/providers/aws/guide/serverless.yml/).
