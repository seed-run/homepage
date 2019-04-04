---
layout: docs
title: Customizing your IAM Policy
---

Seed manages the serverless project in your AWS account on behalf of the IAM user that you create. This means that you need to specify the permissions Serverless Framework needs to deploy your project.

Since the permissions that Serverless Framework needs depends on the services that are being deployed. Let's take a look at the least amount of permissions that needs to be granted for your project give that you are deploying Lambda and API Gateway.

``` json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "cloudformation:CreateStack",
        "cloudformation:Describe*",
        "cloudformation:ValidateTemplate",
        "cloudformation:UpdateStack",
        "cloudformation:List*"
      ],
      "Resource": [
        "arn:aws:cloudformation:<region>:<account_no>:stack/<service_name>*/*"
      ]
    },
    {
      "Effect": "Allow",
      "Action": [
        "s3:*"
      ],
      "Resource": [
        "arn:aws:s3:::<s3_bucket_name>/*"
      ]
    },
    {
      "Effect": "Allow",
      "Action": [
        "logs:DescribeLogGroups"
      ],
      "Resource": [
        "arn:aws:logs:<region>:<account_no>:log-group::log-stream:*"
      ]
    },
    {
      "Effect": "Allow",
      "Action": [
        "logs:CreateLogGroup",
        "logs:CreateLogStream",
        "logs:DeleteLogGroup",
        "logs:DeleteLogStream",
        "logs:DescribeLogStreams",
        "logs:FilterLogEvents"
      ],
      "Resource": [
        "arn:aws:logs:<region>:<account_no>:log-group:/aws/lambda/<service_name>*:log-stream:*"
      ]
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
        "apigateway:*"
      ],
      "Resource": [
        "arn:aws:apigateway:<region>::/restapis",
        "arn:aws:apigateway:<region>::/restapis/<api_id>/*"
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
    }
  ]
}
```

Make sure to replace `<region>`, `<account_no>`, `<service_name>`, `<s3_bucket_name>`, and `<api_id>` for your specific project.

- The `<account_no>` is your AWS Account ID and you can [follow these instructions](http://docs.aws.amazon.com/IAM/latest/UserGuide/console_account-alias.html) to look it up.

- The `<s3_bucket_name>`, is where Serverless Framework stores your builds. You can create this before hand and specifiy this in your `serverless.yml`.

- Also, recall that the `<region>` and `<service_name>` are defined in your `serverless.yml` like so.

  ``` yaml
  service: my-service
  
  provider:
    name: aws
    region: us-east-1
    deploymentBucket: sls-deployment-bucket-001
  ```
  
  In the above `serverless.yml`, the `<region>` is `us-east-1`, the `<service_name>` is `my-service`, and the `<s3_bucket_name>` is `sls-deployment-bucket-001`.
  
- The `<api_id>` is if you have API Gateway deployed as a part of your Serverless project. If you have deployed your project in the past, you can get this by looking at the deployed endpoint. For example, given the following API Gateway endpoint:

  ```
  https://n5z17getxh.execute-api.us-east-1.amazonaws.com/dev
  ```
  
  The `<api_id>` in this case is `n5z17getxh`. You can read more about it [here](https://docs.aws.amazon.com/apigateway/latest/developerguide/how-to-call-api.html).

If you need any help setting this up, you can always [contact us](mailto:{{ site.email }}) directly.

The above provides sufficient permissions for a minimal Serverless project. However, if you provision any additional resources in your `serverless.yml`, or install Serverless plugins, or invoke any AWS APIs in your application code; you would need to update the IAM policy to accommodate for those changes.

Finally, if you are looking for details on where this policy comes from; here is an in-depth discussion on the minimal [Serverless IAM Deployment Policy](https://github.com/serverless/serverless/issues/1439) required for a Serverless project.
