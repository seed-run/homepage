---
layout: build-errors
title: CloudFormation cannot update a stack when a custom-named resource requires replacing
image: /assets/social-cards/common-errors.png
description: CloudFormation cannot update a stack when a custom-named resource requires replacing. Rename xxxxxx-dev and update the stack again.
---

#### Error Message

> XXXXXXXX - CloudFormation cannot update a stack when a custom-named resource requires replacing. Rename xxxxxx-dev and update the stack again.


#### Problem

You've made some changes to a resource, and CloudFormation needs to replace the resource by removing and recreating it. However, CloudFormation cannot replace a resource that has a custom name.


#### Solution

To get around this limitation, you have to rename the resource in your `serverless.yml`, deploy it, and rename it back.

Let's say the resource is called `usersTable-dev`, rename it to `usersTable2-dev` and deploy.

After the deployment succeeds, you can rename the resource back to `usersTable-dev` and continue deploying.

Important: If the resource you are renaming is a DynamoDB table, renaming it will drop all the data. Make sure to back up the table data before renaming and redeploying.
