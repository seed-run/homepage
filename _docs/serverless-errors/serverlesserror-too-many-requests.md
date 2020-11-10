---
layout: common-errors
title: "ServerlessError: Too Many Requests"
image: /assets/social-cards/common-errors.png
description: "ServerlessError: Too Many Requests"
---

#### Error Message

> ServerlessError: Too Many Requests


#### Problem

This is an AWS rate limit error. And can be caused by multiple AWS services. Use the verbose flag, `serverless deploy -v` or `serverless remove -v` to find out which service is being rate limited.

#### Solution

Based on the service that is causing the error, you can figure out if the rate limit can be raised or if it's a hard limit. You can then either request a limit increase or you might have to work around it.

In the case of API Gateway being rate limited while trying to remove a custom domain from an endpoint, [Seed automatically retries the remove process for you]({% link _docs/auto-retrying-serverless-errors.md %}#auto-retrying-on-remove).
