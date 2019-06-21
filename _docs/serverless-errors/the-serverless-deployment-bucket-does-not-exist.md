---
layout: build-errors
title: The serverless deployment bucket does not exist
image: /assets/social-cards/common-errors.png
description: "Could not locate deployment bucket. Error: The specified bucket does not exist"
---

#### Error Message

You might see one of the following error messages:

> The specified bucket does not exist

> Could not locate deployment bucket. Error: The specified bucket does not exist

> The serverless deployment bucket "test-bucket-not-a-serverlessdeploymentbuck-abcd123" does not exist. Create it manually if you want to reuse the CloudFormation stack "test-helper-bucket-not-exist-dev", or delete the stack if it is no longer required.


#### Problem

Serverless Framework creates an S3 bucket to store the deployment artifacts for your Serverless application. In this case, Serverless Framework found the previously deployed CloudFormation stack for your app, but could not find the related S3 bucket.

This can happen if you had previously tried to remove this service and for some reason the removal process failed. Or if the S3 bucket has been manually removed.


#### Solution

You have two options:

1. Delete the CloudFormation stack that has been previously deployed. You would need to manually do this by going to the CloudFormation section of your AWS console. By deleting this, you are effectively starting from scratch. Now try running `serverless deploy` to deploy the service again. Note: if you have an API Gateway endpoint in your serverless.yml, the endpoint will change when deployed from scratch again.

2. If removing the previously deployed resources is not an option, try recreating the S3 bucket, and then run `serverless deploy` again. Just make sure to use the exact name as specified in the error message.
