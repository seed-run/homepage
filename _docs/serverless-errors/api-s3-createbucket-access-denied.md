---
layout: build-errors
title: "API: s3:CreateBucket Access Denied"
image: /assets/social-cards/common-errors.png
description: "ServerlessDeploymentBucket - API: s3:CreateBucket Access Denied."
---

#### Error Message

> ServerlessDeploymentBucket - API: s3:CreateBucket Access Denied.

#### Problem

Serverless Framework creates an S3 bucket to store the deployment artifacts for your Serverless application. This error usually happens when the IAM credentials you are using to deploy doesn't have the permission to create the deployment bucket.


#### Solution

Review the IAM permissions available for the IAM user/role used to deploy your application. And ensure that the `s3:CreateBucket` permission has been granted.
