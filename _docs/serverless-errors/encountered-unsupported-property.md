---
layout: build-errors
title: Encountered unsupported property
image: /assets/social-cards/common-errors.png
description: ApiGatewayRestApi - Encountered unsupported property StageName.
---

#### Error Message

> ApiGatewayRestApi - Encountered unsupported property StageName.


#### Problem

This error happens when the resources defined in your `serverless.yml` has attributes not supported by CloudFormation. Or the resource attributes exported in the stack are not supported by CloudFormation.

For newly introduced resource attributes, they are initially available only via the AWS API, and are only later added to CloudFormation.


#### Solution

Double-check the attribute name against the CloudFormation documentation for the given resource. You can find all the CloudFormation supported resources and attributes over [on the AWS docs](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-template-resource-type-ref.html).

If you want to include resources or resources with attributes that are not available to CloudFormation yet, you have to include them as custom resources. You can read more [on custom resources here](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-custom-resources.html).
