---
layout: build-errors
title: "Template format error: Unresolved resource dependencies in the Resources block of the template"
image: /assets/social-cards/common-errors.png
description: "The CloudFormation template is invalid: Template format error: Unresolved resource dependencies [ApiGatewayRestApi] in the Resources block of the template"
---

#### Error Message

> "The CloudFormation template is invalid: Template format error: Unresolved resource dependencies [ApiGatewayRestApi] in the Resources block of the template"


#### Problem

When you define a resource in your `serverless.yml`, you can reference an attribute of another resource dynamically.

This error happens when the referenced resource cannot be found.


#### Solution

Ensure you are referring to the logical ID of the resource. For example, if you define an S3 bucket in your resources:

``` yml
...

resources:
  Resources:
    S3Bucket:
      Type: AWS::S3::Bucket
      Properties:
        BucketName: my-bucket

...
```

You can reference the name of the bucket with `Ref: S3Bucket`. Do not use the physical ID, `Ref: my-bucket`.
