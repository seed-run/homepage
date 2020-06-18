---
layout: common-errors
title: "Template format error: Number of resources is greater than maximum allowed"
image: /assets/social-cards/common-errors.png
description: "The CloudFormation template is invalid: Template format error: Number of resources, 201, is greater than maximum allowed, 200"
---

#### Error Message

> The CloudFormation template is invalid: Template format error: Number of resources, 201, is greater than maximum allowed, 200


#### Problem

CloudFormation has a hard limit of 200 resources that can be set in a CloudFormation template.

It can be tricky to get a sense of the number of resources just by looking at your `serverless.yml`. For example, if you have 2 Lambda functions with 1 API endpoint, it might seem like you have 3 resources. But apart from the Lambda function and the API Gateway endpoint; an S3 bucket is created to store Lambda code, an IAM role to run the code, CloudWatch log groups to store execution logs, Lambda versions for storing revisions, an API Gateway deployment resource, etc. You quickly end up with a lot more resources than you expect, causing you to go over the limit.

#### Solution

A good practice to get around this is to split up your large service into multiple microservices. You essentially group all your Lambdas and resources by functionality or by type, and each group can be turned into a separate service.

For example, you can move all user related APIs to the users-api service. Or move all search related Lambdas to the search-api service. And DynamoDB tables to the infrastructure service.

This not only gets around the 200 resource limit, but also makes your deployment process a lot faster.

We talk about this in detail in a chapter on [Organizing Serverless Projects](https://serverless-stack.com/chapters/organizing-serverless-projects.html) over on [Serverless Stack](https://serverless-stack.com). We also have a repo with [a sample monorepo serverless app here](https://github.com/AnomalyInnovations/serverless-stack-demo-mono-api).
