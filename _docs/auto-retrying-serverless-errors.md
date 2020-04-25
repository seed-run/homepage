---
layout: docs
title: Auto-Retrying Serverless Errors
---

When using Serverless Framework to continually auto-deploy branches and PRs, you might tend to run into a few issues. These issues can happen intermittently but the CloudFormation deployment might fail, leaving your stack in an unusable state. Meaning that you'll need to completely remove the service before trying again.

This can be annoying, especially if the deployments are completely automated. Since they leave your pipeline in a state that requires manual intervention. At Seed we see a lot of these types of issues from our users and we make it a point to build the retrying capability into our pipelines. This makes them far more resilient to such issues and less likely to need manual intervention.

Currently, Seed auto-retries two types of Serverless Framework errors.

### Auto-Retrying on Deploy

Seed will retry a deployment (ie. `serverless deploy`) if it fails due to CloudFormation not being able to create a new `AWS::ApiGateway::Deployment` resource for your API Gateway endpoint.

This error happens when multiple Serverless services that share the same API Gateway project are being deployed concurrently.

It's because Serverless Framework creates an `AWS::ApiGateway::Deployment` resource in the CloudFormation stack. And when multiple services are being deployed concurrently, multiple `AWS::ApiGateway::Deployment` resources are created against the same API Gateway project, resulting in the above error. These resources are usually created very quickly, so this error happens quite rarely.

When `serverless deploy` fails, Serverless Framework might display one of two errors:

> An error occurred: ApiGatewayDeploymentxxxxxx - Another Deployment is in progress for rest api with id xxxxxxxx. Please try again later. (Service: AmazonApiGateway; Status Code: 409; Error Code: ConflictException; Request ID: xxxx-xxxx-xxxx-xxxx-xxxx).

> ApiGatewayDeploymentxxxxxx - No integration defined for method (Service: AmazonApiGateway; Status Code: 400; Error Code: BadRequestException; Request ID: xxxx-xxxx-xxxx-xxxx-xxxx).

When Seed detects these errors, it'll retry the deployment up to 3 times with a 10, 20 and 30 second backoff respectively.

Note, when this error happens on initial deployments. The CloudFormation stack can end up in the `ROLLBACK_COMPLETE` state. In which case the stack has to be removed before deploying. In this case, Seed **will automatically remove** the stack before redeploying. Seed only does this on initial deployments. It'll not try to remove the stack if it has been previously successfully deployed.

### Auto-Retrying on Remove

Seed will retry removing a service if the removal (ie. `serverless remove`) fails when CloudFormation is throttling API calls. This happens as a result of Serverless Framework repeatedly checking the stack removal progress.

This error happens when multiple Serverless services are being removed concurrently.

Specifically, it happens because Serverless Framework makes a series of `describeStackEvents` API requests to CloudFormation to poll for the removal status. And when multiple services are being removed concurrently, multiple of these calls are made at the same time, resulting in the above error as CloudFormation throttles the API requests.

The error message might look like:

> Serverless Error: Rate exceeded

When Seed detects this error, it'll retry the removal up to 3 times with a 10, 20 and 30 second backoff respectively.

