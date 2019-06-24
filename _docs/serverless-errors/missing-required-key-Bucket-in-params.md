---
layout: build-errors
title: Missing required key 'Bucket' in params
image: /assets/social-cards/common-errors.png
description: Missing required key 'Bucket' in params
---

#### Error Message

> Missing required key 'Bucket' in params


#### Problem

Serverless Framework creates an S3 bucket to store the deployment artifacts for your Serverless application. This error usually happens if the first `serverless deploy` command failed to create the S3 bucket. This in turn will cause all the subsequent deployments to fail with the above error.

There are two common reasons for the S3 bucket failing to create:

1. [IAM credentials not having permission to create S3 buckets]({% link _docs/serverless-errors/api-s3-createbucket-access-denied.md %})
2. [Your AWS account reaches the 100 S3 bucket limit]({% link _docs/serverless-errors/you-have-attempted-to-create-more-buckets-than-allowed.md %})

The two above failures have two error messages that look like:

```
You have attempted to create more buckets than allowed.
```

or

```
s3:CreateBucket Access Denied.
```

Check your first failed deployment for these error messages.

#### Solution

First, identify and fix the issue that caused the initial failure. Here is how to fix [the IAM issue]({% link _docs/serverless-errors/api-s3-createbucket-access-denied.md %}) and [the bucket limit issue]({% link _docs/serverless-errors/you-have-attempted-to-create-more-buckets-than-allowed.md %}).

Then, go over to your CloudFormation console and manually remove the stack. Note: a `serverless remove` might fail with the same error and might not actually remove the stack.

After the stack is done removing, try deploying again.
