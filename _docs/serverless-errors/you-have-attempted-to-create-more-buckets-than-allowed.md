---
layout: common-errors
title: You have attempted to create more buckets than allowed
image: /assets/social-cards/common-errors.png
description: ServerlessDeploymentBucket - You have attempted to create more buckets than allowed.
---

#### Error Message

> ServerlessDeploymentBucket - You have attempted to create more buckets than allowed.


#### Problem

There is a soft limit of 100 S3 buckets per AWS account. You can read more about [the limits here](https://docs.aws.amazon.com/AmazonS3/latest/dev/BucketRestrictions.html).


#### Solution

A quick fix is to remove unused S3 buckets.

If you need additional buckets, submit a support ticket to increase your limit. However, there is a hard limit of 1000 S3 buckets per account.
