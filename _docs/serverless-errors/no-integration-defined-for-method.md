---
layout: common-errors
title: No integration defined for method
image: /assets/social-cards/common-errors.png
description: "ApiGatewayDeploymentxxxxxx - No integration defined for method (Service: AmazonApiGateway; Status Code: 400; Error Code: BadRequestException; Request ID: xxxx-xxxx-xxxx-xxxx-xxxx)."
---

#### Error Message

> ApiGatewayDeploymentxxxxxx - No integration defined for method (Service: AmazonApiGateway; Status Code: 400; Error Code: BadRequestException; Request ID: xxxx-xxxx-xxxx-xxxx-xxxx).


#### Problem

People have reported different scenarios where this could happen. If you haven't manually changed the API Gateway project configuration in the console, this most likely is not an issue with your app.

It can happen when multiple Serverless services that share the same API Gateway project are deployed concurrently. When you add a new API sub-path in one of your services, Serverless Framework tries to create an `AWS::ApiGateway::Method` resource. If another service is deployed while CloudFormation is still in the middle of creating the `AWS::ApiGateway::Method` resource, you'll get the above error. Since Serverless Framework creates an `AWS::ApiGateway::Deployment` resource for that same API Gateway project while it's still being updated.

Note that, the above is not a very common error but is more likely to happen when a stack is first created and the services invloved are being deployed concurrently.


#### Solution

If your deployment failed because you were concurrently deploying your services, you'll need to retry the deployment.

1. Check if the CloudFormation stack is in the `ROLLBACK_COMPLETE` state.

2. If it is, then you'll need to remove the stack from the CloudFormation console before proceeding. You cannot update a stack that's in the `ROLLBACK_COMPLETE` state, you'll get the following error if you do.

   ```
   Stack:arn:aws:cloudformation:us-xxxx-x:xxxxxxxxx:stack/xxx-xx-prod/xxxx-xxxx-xxxx-xxxx-xxxx is in ROLLBACK_COMPLETE state and can not be updated.
   ```

3. After the stack has been removed you can try deploying the service again.

Note that, [Seed](/) will do the above automatically. It'll check the CloudFormation stack status, remove the stack if necessary, and retry the deployment (up to 3 times). You can [read more about this here]({% link _docs/auto-retrying-serverless-errors.md %}#auto-retrying-on-deploy).
