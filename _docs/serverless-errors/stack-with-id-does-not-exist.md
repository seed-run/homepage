---
layout: common-errors
title: Stack with id does not exist
image: /assets/social-cards/common-errors.png
description: Stack with id xxxxxx does not exist
---

#### Error Message

You might see one of the following error messages:

> Stack with id xxxxxx does not exist

> Stack xxxxxx does not exist

#### Problem

A couple of common causes for this error:

1. Serverless Framework was not able to find the previously deployed CloudFormation stack for your Serverless app. This can happen if you had tried to remove the app in the past but the remove failed. Or if the CloudFormation stack for this app has been manually removed.

2. If this error happens on the first deployment; it could be because you are hitting the 100 S3 buckets limit. There is a soft limit of 100 S3 buckets per AWS account. You can read more about [the limits here](https://docs.aws.amazon.com/AmazonS3/latest/dev/BucketRestrictions.html). The reason it shows up as this error is because on the first deployment Serverless Framework tries to create an S3 bucket to store the deployment artifacts. The bucket creation step fails due to the limit. Upon failure, Serverless Framework tries to remove the CloudFormation stack for the service. However, the stack has not yet been created, resulting in this error.

3. You are internally referencing a CloudFormation stack output in your `serverless.yml` using the `${cf:stackName.outputKey}` syntax. And Serverless Framework is not able to find the referenced stack.

#### Solution

##### Problem #1

Manually delete the S3 deployment bucket created by Serverless Framework. This effectively allows you to start over. The S3 bucket should contain the name of your service, the stage you deployed to, and the phrase `serverlessdeploymentbucket`. It should look something like: `my-service-dev-serverlessdeploymentbucket-frinv5ed98h1`.

Once the bucket has been removed, try deploying again.

##### Problem #2

You need to fix the bucket limit issue. A quick fix for this is to remove any unused S3 buckets. If you need additional buckets, submit a support ticket to increase your limit. Note that, there is a hard limit of 1000 S3 buckets per account.

##### Problem #3

The `${cf:stackName.outputKey}` syntax in your `serverless.yml` is resolved before Serverless Framework deploys your service. So you need to make sure that the referenced stack has already been successfully deployed.
