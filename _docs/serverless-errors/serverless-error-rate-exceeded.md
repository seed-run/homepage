---
layout: common-errors
title: "Serverless Error: Rate exceeded"
image: /assets/social-cards/common-errors.png
description: "Serverless Error: Rate exceeded"
---

#### Error Message

> Serverless Error: Rate exceeded


#### Problem

This error happens when multiple Serverless services are being removed concurrently.

It happens because Serverless Framework makes a series of `describeStackEvents` API requests to CloudFormation to poll for the removal status. And when multiple services are being removed concurrently, multiple of these calls are made at the same time, resulting in the above error if CloudFormation throttles the API requests.

Note, this does not mean the removal of the CloudFormation stack has failed.


#### Solution

If your deployment failed because you were concurrently removing your services, you need to try removing the service again. But before you can do that, you'll need to:

1. Check if the CloudFormation stack is in the `DELETE_IN_PROGRESS` state.

2. If it is, then you'll need to wait till the stack removal finishes

3. After the stack removal has finished, and the stack has failed to remove, you can try removing the service again.

Note that, [Seed](/) will do the above automatically. It'll check the CloudFormation stack status, and retry the removal (for a maximum of 3 times). You can [read more about this here]({% link _docs/auto-retrying-serverless-errors.md %}#auto-retrying-on-remove).
