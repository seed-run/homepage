---
layout: common-errors
title: Profile does not exist
image: /assets/social-cards/common-errors.png
description: Profile xxxxx-xxxxxx does not exist
---

#### Error Message

> Profile xxxxx-xxxxxx does not exist


#### Problem

Serverless Framework uses the default AWS profile defined in your `~/.aws/credentials` to deploy your service. You can pick a different profile to use by specifying it in your `serverless.yml`:

``` yml
...

provider:
  profile: account-production

...
```

If the specified profile is not found in your `~/.aws/credentials`, you will get this error.

#### Solution

If a profile has not been added to your `~/.aws/credentials`, you can add it by running `aws configure`.

Alternatively, you can add it manually by adding the following to the bottom of the `~/.aws/credentials` file.

```
[account-production]
aws_access_key_id=AKIAI44QH8DHBEXAMPLE
aws_secret_access_key=je7MtGbClwBF/2Zp9Utk/h3yCo8nvbEXAMPLEKEY
````
