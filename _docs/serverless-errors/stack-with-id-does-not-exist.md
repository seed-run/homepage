---
layout: build-errors
title: Stack with id does not exist
image: /assets/social-cards/common-errors.png
description: Stack with id xxxxxx does not exist
---

#### Error Message

You might see one of the following error messages:

> Stack with id xxxxxx does not exist

> Stack xxxxxx does not exist

#### Problem

Two common causes:

1. Serverless Framework was not able to find the previously deployed CloudFormation stack for your Serverless app. This can happen if you had tried to remove the app in the past but the remove failed. Or if the CloudFormation stack for this app has been manually removed.

2. If this is happening on the first deployment, this can happen if you are hitting the 100 S3 buckets limit. There is a soft limit of 100 S3 buckets per AWS account. You can read more about [the limits here](https://docs.aws.amazon.com/AmazonS3/latest/dev/BucketRestrictions.html). What happened is that on the first deployment Serverless Framework tries to create an S3 bucket to store deployment artifacts, and the creation fails due to the limit. On failure, Serverless Framework tries to remove the CloudFormation stack for the service. However, the stack has not yet been created yet, and hence the error.

#### Solution to Problem #1

Manually delete the S3 deployment bucket created by Serverless Framework. This effectively allows you to start over. The S3 bucket should contain the name of your service, the stage you deployed to, and the phrase `serverlessdeploymentbucket`. It should look something like: `my-service-dev-serverlessdeploymentbucket-frinv5ed98h1`.

Once the bucket has been removed, try deploying again.

#### Solution to Problem #2

A quick fix is to remove unused S3 buckets.

If you need additional buckets, submit a support ticket to increase your limit. However, there is a hard limit of 1000 S3 buckets per account.
