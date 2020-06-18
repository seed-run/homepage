---
layout: common-errors
title: User is not authorized to perform action on resource
image: /assets/social-cards/common-errors.png
description: "User: arn:aws:iam::xxxxxxxxxxxxx:user/xxxxx-xxxxx is not authorized to perform: cloudformation:DescribeStacks on resource: arn:aws:cloudformation:us-xxxx-x:xxxxxxxxx:stack/my-service-dev/*"
---

#### Error Message

> "User: arn:aws:iam::xxxxxxxxxxxxx:user/xxxxx-xxxxx is not authorized to perform: cloudformation:DescribeStacks on resource: arn:aws:cloudformation:us-xxxx-x:xxxxxxxxx:stack/my-service-dev/*"


#### Problem

The AWS credentials you are using does not have enough permissions to deploy your service.


#### Solution

The error message includes the specific IAM permission that is missing to continue the deployment. Go to the IAM console and grant that permission to the IAM user/role you are using to deploy your service.

If you are not familiar with how AWS IAM works and you just want to deploy a test project to see your app in action, you can go with the `AdministratorAccess` permission. It's guaranteed to contain all the required permissions to deploy your service.

Note that, it's not recommended to use `AdministratorAccess` in a production environment. Instead, figure out the least set of permissions that are required for your app. We have [a more detailed article on this here]({% link _docs/customizing-your-iam-policy.md %}).
