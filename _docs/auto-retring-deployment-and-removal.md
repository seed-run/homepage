---
layout: docs
title: Auto-Retrying Deployment and Removal
---

### Auto-Retrying on Deploy

Seed will retry deploying if deployment (ie. `serverless deploy`) failed due to CloudFormation failed to a new `AWS::ApiGateway::Deployment` resource for your API Gateway endpoint.

This error happens when multiple Serverless services that share the same API Gateway project are being deployed concurrently.

It happens because Serverless Framework creates an AWS::ApiGateway::Deployment resource in the CloudFormation stack. And when multiple services are being deployed concurrently, multiple of these AWS::ApiGateway::Deployment resources are created against the same API Gateway project, resulting in the above error. These resources are usually created very quickly, so this error happens quite rarely.

When `serverless deploy` fails, Serverless Framework can display one of two errors below:

> An error occurred: ApiGatewayDeploymentxxxxxx - Another Deployment is in progress for rest api with id xxxxxxxx. Please try again later. (Service: AmazonApiGateway; Status Code: 409; Error Code: ConflictException; Request ID: xxxx-xxxx-xxxx-xxxx-xxxx).

> ApiGatewayDeploymentxxxxxx - No integration defined for method (Service: AmazonApiGateway; Status Code: 400; Error Code: BadRequestException; Request ID: xxxx-xxxx-xxxx-xxxx-xxxx).


When the error is detected, Seed will retry the deployment up to 3 times with 10, 20 and 30 seconds backoff between the retries.

Note, when this error happens on the initial deployment, the CloudFormation stack can end up in the ROLLBACK_COMPLETE state. In which case the stack as to be removed before further deployment. In this case, Seed will automatically remove the stack before redeploying. Seed only does this when initial deployment fails. Seed will not try to removal stack that has been preivously successfully deployed.

### Auto-Retrying on Remove

Seed will retry removing a service if removal (ie. `serverless deploy`) failed due to CloudFormation throttled API calls made by Serverless Framwework when checking removal progress.

This error happens when multiple Serverless services are being removed concurrently.

It happens because Serverless Framework makes a series of `describeStackEvents` API requests to CloudFormation to poll for the removal status. And when multiple services are being removed concurrently, multiple of these calls are made at the same time, resulting in the above error if CloudFormation throttles the API requests.

When the error is detected, Seed will retry the removal up to 3 times with 10, 20 and 30 seconds backoff between the retries.

