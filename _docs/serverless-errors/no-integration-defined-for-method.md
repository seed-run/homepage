---
layout: build-errors
title: No integration defined for method
image: /assets/social-cards/common-errors.png
description: "ApiGatewayDeploymentxxxxxx - No integration defined for method (Service: AmazonApiGateway; Status Code: 400; Error Code: BadRequestException; Request ID: xxxx-xxxx-xxxx-xxxx-xxxx)."
---

#### Error Message

> ApiGatewayDeploymentxxxxxx - No integration defined for method (Service: AmazonApiGateway; Status Code: 400; Error Code: BadRequestException; Request ID: xxxx-xxxx-xxxx-xxxx-xxxx).


#### Problem

People have reported different scenarios where this could happen. If you have not manually changed the API Gateway project configuration in the console, this most likely is not an issue with your app.


#### Solution

There are a couple of solutions that worked for people depending on the cause. We've listed them out in the order starting with the ones are least likely to impact your deployed resources:

1. Update your Serverless Framework to v1.30.3 or later and try deploying again.

2. If your Lambdas have http events with cors enabled, turn off cors by removing `cors: true` from your `serverless.yml` and try deploying the service again. After the deployment succeeds, put the `cors: true` option back and deploy again.

3. Remove all http events from your Lambda definitions and try deploying the service again. This will remove the API Gateway project entirely. After the deployment succeeds, put the http events back and deploy again. Note that, removing and redeploying will result in a different API Gateway endpoint.

4. If removing the service is an option for you, run `serverless remove` to remove the service entirely. Ensure all API Gateway resources have been successfully removed in the API Gateway console. Then deploy the service again.
