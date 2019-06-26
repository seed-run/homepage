---
layout: build-errors
title: "The requested resource exceeds the maximum number allowed. (Service: AmazonCloudWatchEvents)"
image: /assets/social-cards/common-errors.png
description: "xxxxxxxx - The requested resource exceeds the maximum number allowed. (Service: AmazonCloudWatchEvents)"
---

#### Error Message

> "xxxxxxxx - The requested resource exceeds the maximum number allowed. (Service: AmazonCloudWatchEvents)"


#### Problem

There is a soft limit of 100 CloudWatch rules per region per account. Here is some more info on all [the CloudWatch Events limits](https://docs.aws.amazon.com/AmazonCloudWatch/latest/events/cloudwatch_limits_cwe.html).


#### Solution

To get around the limit, you can try removing unused CloudWatch rules.

Or if you need to create additional rules, submit a support ticket to increase your CloudWatch rules limit.
