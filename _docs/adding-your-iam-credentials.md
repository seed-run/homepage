---
layout: docs
title: Adding your IAM Credentials
---

[Seed](/) needs your AWS IAM credentials to deploy your project on your behalf to your AWS account.

The IAM permissions that Seed requires is made up of:

1. The permissions that Seed needs
2. And the permissions SST or Serverless Framework needs to deploy your app

Seed can help you create an IAM role with the necessary credentials. Hit the **Help me create an IAM Role** link.

![Click the help me create an IAM role link screenshot](/assets/docs/iam/click-the-help-me-create-an-iam-role-link.png)

Review the permissions that Seed needs.

![Review Seed IAM permissions screenshot](/assets/docs/iam/review-seed-iam-permissions.png)

For reference here are the permissions Seed needs.

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "ManagePromoteChangeset",
      "Effect": "Allow",
      "Action": [
        "cloudformation:GetTemplate",
        "cloudformation:CreateChangeSet",
        "cloudformation:DescribeChangeSet"
      ],
      "Resource": [
        {
          "Fn::Sub": "arn:aws:cloudformation:*:${AWS::AccountId}:*"
        }
      ]
    },
    {
      "Sid": "ManageDeployedResources",
      "Effect": "Allow",
      "Action": [
        "cloudformation:GetTemplate",
        "cloudformation:ListStacks",
        "cloudformation:ListStackResources",
        "cloudformation:DescribeStacks",
        "apigateway:GET"
      ],
      "Resource": "*"
    },
    {
      "Sid": "MonitorLogs",
      "Effect": "Allow",
      "Action": [
        "apigateway:GET",
        "lambda:GetFunction",
        "logs:DescribeLogStreams",
        "logs:FilterLogEvents",
        "logs:GetLogEvents",
        "logs:GetQueryResults",
        "logs:StartQuery",
        "logs:StopQuery"
      ],
      "Resource": "*"
    },
    {
      "Sid": "MonitorMetrics",
      "Effect": "Allow",
      "Action": [
        "apigateway:GET",
        "cloudwatch:GetMetricData",
        "cloudformation:ListStackResources"
      ],
      "Resource": "*"
    },
    {
      "Sid": "ManageIssues",
      "Effect": "Allow",
      "Action": [
        "cloudformation:ListStackResources",
        "cloudformation:DescribeStacks",
        "logs:CreateLogGroup",
        "logs:DescribeSubscriptionFilters",
        "logs:PutSubscriptionFilter",
        "logs:DeleteSubscriptionFilter",
        "lambda:GetFunction"
      ],
      "Resource": "*"
    },
    {
      "Sid": "ManageAPICustomDomain",
      "Effect": "Allow",
      "Action": [
        "iam:CreateServiceLinkedRole",
        "route53:ListHostedZones",
        "route53:ListResourceRecordSets",
        "route53:ChangeResourceRecordSets",
        "acm:ListCertificates",
        "acm:AddTagsToCertificate",
        "acm:RequestCertificate",
        "acm:DescribeCertificate",
        "acm:DeleteCertificate",
        "apigateway:GET",
        "apigateway:POST",
        "apigateway:DELETE",
        "cloudfront:UpdateDistribution"
      ],
      "Resource": "*"
    },
    {
      "Sid": "ManageAPIAccessLog",
      "Effect": "Allow",
      "Action": [
        "iam:CreateRole",
        "apigateway:GET",
        "apigateway:PATCH",
        "logs:CreateLogGroup",
        "logs:DescribeLogGroups"
      ],
      "Resource": "*"
    },
    {
      "Sid": "ManageAPIAccessLogIam",
      "Effect": "Allow",
      "Action": ["iam:AttachRolePolicy", "iam:PassRole"],
      "Resource": [
        {
          "Fn::Sub": "arn:aws:iam::${AWS::AccountId}:role/APIGatewayLogsRole*"
        }
      ]
    }
  ]
}
```

Next, customize the permissions that SST or Serverless Framework needs to deploy your app. By default these permissions are very broad since this depends specifically on your app. If you are already using a set of IAM permissions to deploy, you can paste them here.

![Customize deploy IAM permissions screenshot](/assets/docs/iam/customize-deploy-iam-permissions.png)

Alternatively, you can read the [Customizing your IAM Policy]({% link _docs/customizing-your-iam-policy.md %}) chapter; to get a better idea on how to craft an airtight policy.

Once you are done customizing the permissions, Seed will put the two above sets of permissions together. And will help you create an IAM role using CloudFormation.

Hit the **Create an IAM role using CloudFormation** button.

![Click Create an IAM role using CloudFormation screenshot](/assets/docs/iam/click-create-an-iam-role-using-cloudformation.png)

This will redirect you to CloudFormation on your AWS Console.

![CloudFormation Seed template screenshot](/assets/docs/iam/cloudformation-seed-template.png)

Scroll down to the bottom of the page, hit the **I acknowledge that AWS CloudFormation might create IAM resources.** and click **Create**.

![Click create CloudFormation Seed template screenshot](/assets/docs/iam/click-create-cloudformation-seed-template.png)

CloudFormation will now create a Seed IAM role. This will take a minute or two.

![CloudFormation Seed role creating screenshot](/assets/docs/iam/cloudformation-seed-role-creating.png)

Once complete, expand the **Outputs** section. And copy the **RoleArn**.

![CloudFormation complete output screenshot](/assets/docs/iam/cloudformation-complete-output.png)

Paste it back over on Seed.

![Paste IAM credentials on Seed screenshot](/assets/docs/iam/paste-iam-credentials-on-seed.png)

Hit **Add App** to complete creating your app!
