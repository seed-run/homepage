---
layout: build-errors
title: Stack with id does not exist
image: /assets/social-cards/common-errors.png
description: Stack with id xxxxxx does not exist
---

#### Error Message

> Stack with id xxxxxx does not exist


#### Problem

Serverless Framework was not able to find the previously deployed CloudFormation stack for your Serverless app. This can happen if you had tried to remove the app in the past but the remove failed. Or if the CloudFormation stack for this app has been manually removed.

#### Solution

Manually delete the S3 deployment bucket created by Serverless Framework. This effectively allows you to start over. The S3 bucket should contain the name of your service, the stage you deployed to, and the phrase `serverlessdeploymentbucket`. It should look something like: `my-service-dev-serverlessdeploymentbucket-frinv5ed98h1`.

Once the bucket has been removed, try deploying again.
