---
layout: docs
title: Customizing your IAM Policy
---

Seed manages the serverless project in your AWS account on behalf of the IAM user that you create. It is important to grant sufficient permissions to this user.

The permissions required can be categorized into the following areas:

- Permissions required by Seed
- Permissions required by Serverless Framework
- Permissions required by your Serverless Framework plugins
- Permissions required by your Lambda code

Granting **AdministratorAccess** policy ensures that your project will always have the necessary permissions. But if you want to create an IAM policy that grants the minimal set of permissions, you need to customize your IAM policy.

A basic Serverless project in Seed needs permissions to the following AWS services:

- **CloudFormation** to create changeset and update stack
- **S3** to upload and store Serverless artifacts and Lambda source code
- **CloudWatch Logs** to store Lambda execution logs
- **IAM** to manage policies for the Lambda IAM Role
- **API Gateway** to manage API endpoints
- **Lambda** to manage Lambda functions
- **EC2** to execute Lambda in VPC
- **CloudWatch Events** to manage CloudWatch event triggers
- **KMS** for Seed to create and manage the encryption key used to protect your project [secret variables]({% link _docs/storing-secrets.md %})
- **Route53** and **ACM** for Seed to manage your custom domains
- **Logs** for Seed to manage your Lambda and Access logs

### A simple IAM Policy template

These can be defined and granted using a simple IAM policy.

``` json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "cloudformation:*",
        "s3:*",
        "logs:*",
        "iam:*",
        "apigateway:*",
        "lambda:*",
        "ec2:DescribeSecurityGroups",
        "ec2:DescribeSubnets",
        "ec2:DescribeVpcs",
        "events:*",
        "kms:*",
        "route53:*",
        "acm:*",
        "apig:*",
        "logs:*"
      ],
      "Resource": [
        "*"
      ]
    }
  ]
}
```

This policy grants access to all the resources listed above. But we can narrow this down further by restricting them to specific **Actions** for the specific **Resources** in each AWS service.

### An advanced IAM Policy template

Below is a more nuanced policy template that restricts access to the Serverless project that is being deployed. Make sure to replace `<region>`, `<account_no>` and `<service_name>` for your specific project.

``` json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "cloudformation:Describe*",
        "cloudformation:List*",
        "cloudformation:Get*",
        "cloudformation:PreviewStackUpdate",
        "cloudformation:CreateStack",
        "cloudformation:UpdateStack",
        "cloudformation:DeleteStack"
      ],
      "Resource": "arn:aws:cloudformation:<region>:<account_no>:stack/<service_name>*/*"
    },
    {
      "Effect": "Allow",
      "Action": [
        "cloudformation:ValidateTemplate"
      ],
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": [
        "s3:CreateBucket",
        "s3:DeleteBucket",
        "s3:Get*",
        "s3:List*"
      ],
      "Resource": [
        "arn:aws:s3:::*"
      ]
    },
    {
      "Effect": "Allow",
      "Action": [
        "s3:*"
      ],
      "Resource": [
        "arn:aws:s3:::*/*"
      ]
    },
    {
      "Effect": "Allow",
      "Action": [
        "logs:DescribeLogGroups"
      ],
      "Resource": "arn:aws:logs:<region>:<account_no>:log-group::log-stream:*"
    },
    {
      "Action": [
        "logs:CreateLogGroup",
        "logs:CreateLogStream",
        "logs:DeleteLogGroup",
        "logs:DeleteLogStream",
        "logs:DescribeLogStreams",
        "logs:FilterLogEvents"
      ],
      "Resource": "arn:aws:logs:<region>:<account_no>:log-group:/aws/lambda/<service_name>*:log-stream:*",
      "Effect": "Allow"
    },
    {
      "Effect": "Allow",
      "Action": [
        "iam:GetRole",
        "iam:PassRole",
        "iam:CreateRole",
        "iam:DeleteRole",
        "iam:DetachRolePolicy",
        "iam:PutRolePolicy",
        "iam:AttachRolePolicy",
        "iam:DeleteRolePolicy"
      ],
      "Resource": [
        "arn:aws:iam::<account_no>:role/<service_name>*-lambdaRole"
      ]
    },
    {
      "Effect": "Allow",
      "Action": [
        "apigateway:GET",
        "apigateway:POST",
        "apigateway:PUT",
        "apigateway:DELETE"
      ],
      "Resource": [
        "arn:aws:apigateway:<region>::/restapis"
      ]
    },
    {
      "Effect": "Allow",
      "Action": [
        "apigateway:GET",
        "apigateway:POST",
        "apigateway:PUT",
        "apigateway:DELETE"
      ],
      "Resource": [
        "arn:aws:apigateway:<region>::/restapis/*"
      ]
    },
    {
      "Effect": "Allow",
      "Action": [
        "lambda:GetFunction",
        "lambda:CreateFunction",
        "lambda:DeleteFunction",
        "lambda:UpdateFunctionConfiguration",
        "lambda:UpdateFunctionCode",
        "lambda:ListVersionsByFunction",
        "lambda:PublishVersion",
        "lambda:CreateAlias",
        "lambda:DeleteAlias",
        "lambda:UpdateAlias",
        "lambda:GetFunctionConfiguration",
        "lambda:AddPermission",
        "lambda:RemovePermission",
        "lambda:InvokeFunction"
      ],
      "Resource": [
        "arn:aws:lambda:*:<account_no>:function:<service_name>*"
      ]
    },
    {
      "Effect": "Allow",
      "Action": [
        "ec2:DescribeSecurityGroups",
        "ec2:DescribeSubnets",
        "ec2:DescribeVpcs"
      ],
      "Resource": [
        "*"
      ]
    },
    {
      "Effect": "Allow",
      "Action": [
        "events:Put*",
        "events:Remove*",
        "events:Delete*",
        "events:Describe*"
      ],
      "Resource": "arn:aws:events::<account_no>:rule/<service_name>*"
    },
    {
      "Effect": "Allow",
      "Action": [
        "kms:*"
      ],
      "Resource": "arn:aws:kms::<account_no>:key/*"
    },
    {
        "Effect": "Allow",
        "Action": [
            "route53:ChangeResourceRecordSets",
            "route53:ListHostedZones",
            "route53:ListResourceRecordSets"
        ],
        "Resource": "*"
    },
    {
        "Effect": "Allow",
        "Action": [
            "acm:AddTagsToCertificate",
            "acm:RequestCertificate",
            "acm:DescribeCertificate",
            "acm:DeleteCertificate"
        ],
        "Resource": "*"
    },
    {
        "Effect": "Allow",
        "Action": [
            "apig:GetAccount",
            "apig:UpdateAccount",
            "apig:GetResources",
            "apig:GetStage",
            "apig:UpdateStage",
            "apig:CreateDomainName",
            "apig:CreateBasePathMapping",
            "apig:GetDomainNames",
            "apig:GetBasePathMapping",
            "apig:DeleteBasePathMapping"
        ],
        "Resource": "*"
    },
    {
        "Effect": "Allow",
        "Action": [
            "logs:CreateLogGroup",
            "logs:describeLogGroups"
        ],
        "Resource": "arn:aws:logs:<region>:<account_no>:log-group:API-Gateway-Access-Logs_*:log-stream:*"
    }
  ]
}
```

The `<account_no>` is your AWS Account ID and you can [follow these instructions](http://docs.aws.amazon.com/IAM/latest/UserGuide/console_account-alias.html) to look it up.

Also, recall that the `<region>` and `<service_name>` are defined in your `serverless.yml` like so.

``` yaml
service: my-service

provider:
  name: aws
  region: us-east-1
```

In the above `serverless.yml`, the `<region>` is `us-east-1` and the `<service_name>` is `my-service`.

The above IAM policy template restricts access to the AWS services based on the name of your Serverless project and the region it is deployed in.

It provides sufficient permissions for a minimal Serverless project. However, if you provision any additional resources in your **serverless.yml**, or install Serverless plugins, or invoke any AWS APIs in your application code; you would need to update the IAM policy to accommodate for those changes.

Finally, if you are looking for details on where this policy comes from; here is an in-depth discussion on the minimal [Serverless IAM Deployment Policy](https://github.com/serverless/serverless/issues/1439) required for a Serverless project.
