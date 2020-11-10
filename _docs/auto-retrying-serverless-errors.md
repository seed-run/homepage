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

Seed will retry removing a service if the removal (ie. `serverless remove`) fails due to the following errors:

1. [`Rate exceeded`]({% link _docs/serverless-errors/serverless-error-rate-exceeded.md %})

   These errors mean that CloudFormation is throttling API calls. This happens as a result of Serverless Framework repeatedly checking the stack removal progress. Specifically, if multiple Serverless services are being removed concurrently.

   Serverless Framework makes a series of `describeStackEvents` API requests to CloudFormation to poll for the removal status. And when multiple services are being removed concurrently, multiple of these calls are made at the same time, resulting in the above error as CloudFormation throttles the API requests.

2. [`Too Many Requests`]({% link _docs/serverless-errors/serverlesserror-too-many-requests.md %})

   This is a rate limit error that can be caused by multiple services. For example, API Gateway has a hard limit of removing 1 custom domain per account every 30 seconds. Seed will simply retry removing the service.

3. [`The serverless deployment bucket does not exist`]({% link _docs/serverless-errors/the-serverless-deployment-bucket-does-not-exist.md %})

   This error usually happens if the deployment S3 bucket that Serverless Framework uses, has already been removed. In this case Seed will retry the process by removing the CloudFormation template for the stack.

4. [`Export resource cannot be deleted as it is in use`]({% link _docs/serverless-errors/export-resource-cannot-be-deleted-as-it-is-in-use.md %})

   This error can happen when multiple services that depend on each other are being removed. It's usually a timing related issue. Seed will automatically retry the remove process.

Note that, for the above errors Seed will retry the removal process a maximum of 3 times. If you find that you are running into some removal related errors repeatedly, [feel free to contact us](mailto:{{ site.email }}) and we'll look into putting in a fix for it.
