---
layout: build-errors
title: Resource already exist
image: /assets/social-cards/common-errors.png
description: "Resource - xxxxxx already exists in stack arn:aws:cloudformation:xx-xxxx-x:xxxxxxxx:stack/my-service-staging/xxxxxx-xxxx-xxxx--xxxxxxxxxx."
---

#### Error Message

You might see one of the following error messages.

> Resource - xxxxxx already exists.

> Resource - xxxxxx already exists in stack arn:aws:cloudformation:xx-xxxx-x:xxxxxxxx:stack/my-service-staging/xxxxxx-xxxx-xxxx--xxxxxxxxxx.


#### Problem

Serverless failed to deploy because it tried to create a resource with the specified name, and a resource with that name already exists in another stack. Most resource names need to be unique per account per region. While some resource names need to be unique in an account across all regions. And for S3 for example, bucket names need to be unique globally.


#### Solution

Remove the existing resource, if it's no longer needed. If the resource was created by a CloudFormation stack, you would need to remove the entire stack.

If removing the resource is not an option, change the name of the new resource and deploy again. Note: It's a good practice to parameterize the resource name with the name of the stage. This ensures uniqueness when deploying the service to multiple stages, ie. use `usersTable-staging` instead of just `usersTable`.
