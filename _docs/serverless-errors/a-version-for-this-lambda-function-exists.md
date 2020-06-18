---
layout: common-errors
title: A version for this Lambda function exists
image: /assets/social-cards/common-errors.png
description: "An error occurred: xxxxxxxxx - A version for this Lambda function exists ( 1 ). Modify the function to create a new version."
---

#### Error Message

> An error occurred: xxxxxxxxx - A version for this Lambda function exists ( 1 ). Modify the function to create a new version.


#### Problem

This error is caused by Serverless Framework trying to create a new version of your Lambda function when the code has not changed. It detects changes by generating a SHA checksum of the code.

Use of certain Serverless plugins or rare glitches in Serverless Framework could also cause this issue.


#### Solution

Most likely, this is an issue with your code.

A one time workaround for this issue is to make a dummy change in a function's code and deploy again.

If the issue persists, you can try turning off Lambda versioning by setting the following in your `serverless.yml`.

``` yml
...

provider:
  name: aws
  versionFunctions: false

...
```
