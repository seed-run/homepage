---
layout: build-errors
title: Rate exceeded
image: /assets/social-cards/common-errors.png
description: "Rate exceeded"
---

#### Error Message

> Rate exceeded


#### Problem

This error happens when multiple Serverless services are being removed concurrently.

It happens because Serverless Framework makes a series of `describeStackEvents` API requests to CloudFormation to poll for the removal status. And when multiple services are being removed concurrently, multiple of these calls are made at the same time, resulting in the above error if CloudFormation throttles the API requests.

Note this does not mean the removal of the CloudFormation stack has failed.


#### Solution

If your deployment failed because you were concurrently remove your services, you can need to retry the removal.

1. Check if the CloudFormation stack is in the `DELETE_IN_PROGRESS` state.

2. If it is, then you'll need to wait till the stack removal finishes

3. After the stack removal is finished, and the stack has failed to removed, you can try removing the service again.

Note that, [Seed](/) will do the above automatically. It'll check the CloudFormation stack status, and retry the removal (up to 3 times).
