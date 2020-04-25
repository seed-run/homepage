---
layout: build-errors
title: Another Deployment is in progress for rest api with id
image: /assets/social-cards/common-errors.png
description: "An error occurred: ApiGatewayDeploymentxxxxxx - Another Deployment is in progress for rest api with id xxxxxxxx . Please try again later. (Service: AmazonApiGateway; Status Code: 409; Error Code: ConflictException; Request ID: xxxx-xxxx-xxxx-xxxx-xxxx)."
---

#### Error Message

> An error occurred: ApiGatewayDeploymentxxxxxx - Another Deployment is in progress for rest api with id xxxxxxxx. Please try again later. (Service: AmazonApiGateway; Status Code: 409; Error Code: ConflictException; Request ID: xxxx-xxxx-xxxx-xxxx-xxxx).


#### Problem

This error happens when multiple Serverless services that share the same API Gateway project are being deployed concurrently.

It happens because Serverless Framework creates an `AWS::ApiGateway::Deployment` resource in the CloudFormation stack. And when multiple services are being deployed concurrently, multiple  of these `AWS::ApiGateway::Deployment` resources are created against the same API Gateway project, resulting in the above error. These resources are usually created very quickly, so this error happens quite rarely.


#### Solution

If your deployment failed because you were concurrently deploying your services, you'll need to retry the deployment.

1. Check if the CloudFormation stack is in the `ROLLBACK_COMPLETE` state.

2. If it is, then you'll need to remove the stack from the CloudFormation console before proceeding. You cannot update a stack that's in the `ROLLBACK_COMPLETE` state, you'll get the following error if you do.

   ```
   Stack:arn:aws:cloudformation:us-xxxx-x:xxxxxxxxx:stack/xxx-xx-prod/xxxx-xxxx-xxxx-xxxx-xxxx is in ROLLBACK_COMPLETE state and can not be updated.
   ```

3. After the stack has been removed you can try deploying the service again.

Note that, [Seed](/) will do the above automatically. It'll check the CloudFormation stack status, remove the stack if necessary, and retry the deployment (up to 3 times). You can [read more about this here]({% link _docs/auto-retrying-serverless-errors.md %}#auto-retrying-on-deploy).
