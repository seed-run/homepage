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

Let's look at the least amount of permissions that needs to be granted for your project to work on Seed. Below is a nuanced policy template that restricts access to the Serverless project that is being deployed.

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
      "Resource": [
        "arn:aws:cloudformation:<region>:<account_no>:stack/<service_name>*/*"
      ]
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
        "apigateway:*",
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
    },
    {
      "Effect": "Allow",
      "Action": [
        "kms:CreateKey",
        "kms:CreateAlias",
        "kms:ListAliases"
      ],
      "Resource": [
        "*"
      ]
    },
    {
      "Effect": "Allow",
      "Action": [
        "kms:Decrypt",
        "kms:Encrypt"
      ],
      "Resource": [
        "arn:aws:kms:*:<account_no>:key/*"
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

Additionally if you want Seed to set your custom domains for any API Gateway endpoints you might have; add the following blocks to your IAM Role.

``` json
[
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
          "apigateway:GET",
          "apigateway:POST",
          "apigateway:DELETE",
      ],
      "Resource": [
        "arn:aws:apigateway:<region>::/domainnames"
      ]
  }
]
```

And finally, if you'd like Seed to turn on access logs for API Gateway add this as well.

``` json
[
  {
      "Effect": "Allow",
      "Action": [
          "apigateway:GET",
          "apigateway:PATCH",
      ],
      "Resource": [
        "arn:aws:apigateway:<region>::/account"
      ]
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
```


If you need any help setting this up, you can always [contact us](mailto:{{ site.email }}) directly.

The above provides sufficient permissions for a minimal Serverless project. However, if you provision any additional resources in your `serverless.yml`, or install Serverless plugins, or invoke any AWS APIs in your application code; you would need to update the IAM policy to accommodate for those changes.

Finally, if you are looking for details on where this policy comes from; here is an in-depth discussion on the minimal [Serverless IAM Deployment Policy](https://github.com/serverless/serverless/issues/1439) required for a Serverless project.
