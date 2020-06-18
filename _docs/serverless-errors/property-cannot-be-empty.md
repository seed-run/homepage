---
layout: common-errors
title: Property cannot be empty
image: /assets/social-cards/common-errors.png
description: "An error occurred: ApiGatewayStage - Property RestApiId cannot be empty.."
---

#### Error Message

> An error occurred: ApiGatewayStage - Property RestApiId cannot be empty..


#### Problem

This happens when the resources defined in your `serverless.yml` are missing attributes that are required by CloudFormation.


#### Solution

Double-check the attributes against the ones in the CloudFormation documentation for the resource in question. Ensure you have defined all the `Required` attributes. You can find all the CloudFormation supported resources and attributes in [the AWS docs here](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-template-resource-type-ref.html).
