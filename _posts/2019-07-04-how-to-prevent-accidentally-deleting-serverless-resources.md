---
layout: post
title: How to prevent accidentally deleting Serverless resources
image: /assets/social-cards/prevent-accidental-delete.png
description: In this post we'll look at how to prevent Serverless resources from being accidentally deleted by generating change sets, setting the DeletionPolicy to Retain, and enabling stack termination protection.
categories: tips
author: jack
---

If you are using Serverless Framework to deploy your Serverless app, all your resources should be deployed automatically thanks to the infrastructure as code setup. This means that your resources (databases, API endpoints, Lambda functions, etc.) are created, modified, and removed by simply changing your Serverless config.

This might leave you wondering, what happens if I make a mistake in my `serverless.yml` definition? Will my resources get accidentally deleted?

In this post we'll look at how to prevent accidentally deleting Serverless resources.

Let's start with a concrete example. Following is an excerpt from the resources section of a `serverless.yml`.

``` yml
...

  Resources:
    UsersTable:
      Type: AWS::DynamoDB::Table
      Properties:
        TableName: users

...
```

On subsequent deployments, if you have a typo in the `TableName`, ie. `userss`, upon deployment the `users` table will be dropped and a new (and empty) table `userss` with the same schema will be created.

To avoid such issues, you've got a couple of options:

### 1. Review the update change set

The `serverless deploy` command internally runs a `serverless package` to generate the artifacts and then deploys those artifacts. The artifact is made up of your code (as a zip file) and a CloudFormation template (infrastructure as code) that describes the resources for your app.

You can review the infrastructure changes before you deploy:

- Run the `serverless package` command first. This will generate a CloudFormation template.
- Go into your `CloudFormation console`, select the stack for the service you are deploying, click on **Create change set for current stack**, and upload the generated template. You can read more about this in the [AWS docs](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/using-cfn-updating-stacks-changesets-create.html).
- You will get a list of actions CloudFormation will perform on your stack, if you were to deploy them.

You can automate this process by making this a step in your CI/CD pipeline. [Seed](/) does this out of the box. Seed will also highlight the key changes like removing a DynamoDB table or a SNS subscription. And it'll only deploy the changes after you review and confirm them. You can read more about [promoting to production here](https://seed.run/docs/promoting-to-production).

![Seed CloudFormation Change Set](/assets/blog/how-to-prevent-serverless-resources-from-accidental-deletes/seed-cloudformation-changeset.png)

### 2. Retain specific resources

However, there are some resources that you absolutely do not want getting deleted. You can enforce this through CloudFormation.

By default, the **DeletionPolicy** for all resources is set to `Delete`. This means that when a stack is deleted, all its resources are deleted. Set the **DeletionPolicy** to `Retain` on the resources that you want to make sure are not removed through CloudFormation. This is especially useful for the resources that contains data.

To enable the `Retain` flag, change the resource definition (from above) to:

``` yml
 Resources:
  UsersTable:
    Type: AWS::DynamoDB::Table
    DeletionPolicy: Retain
    Properties:
      TableName: users
``` 

### 3. Prevent a stack from being deleted

Finally, you can prevent an entire stack from being deleted by enabling **termination protection**. You can do so in the CloudFormation console:

![CloudFormation change termination protection](/assets/blog/how-to-prevent-serverless-resources-from-accidental-deletes/cloudformation-change-termination-protection.png)

Or alternatively, via the AWS CLI:

``` bash
$ aws cloudformation update-termination-protection –enable-termination-protection –stack-name STACK_NAME
```

#### Summary

You should now have a good idea of how to prevent your Serverless resources from being accidentally deleted. It's advisable to enable on **termination protection** for the production CloudFormation stack while enabling the `Retain` flag for your database tables. And in general, review your change sets before they get promoted to production.
