---
layout: page
title: Adding your IAM Credentials
---

[Seed](/) needs your AWS IAM credentials to deploy your project on your behalf to your AWS account. Follow these steps to generate your credentials.

Log in to your [AWS Console](https://console.aws.amazon.com) and select IAM from the list of services.

![Select IAM Service Screenshot](/assets/docs/iam/select-iam-service.png)

Select **Users**.

![Select IAM Users Screenshot](/assets/docs/iam/select-iam-users.png)

Select **Add User**.

![Add IAM User Screenshot](/assets/docs/iam/add-iam-user.png)

Enter a **User name** and check **Programmatic access**, then select **Next: Permissions**.

This account will be used by Seed. It will be connecting to the AWS API directly and will not be using the Management Console.

![Fill in IAM User Info Screenshot](/assets/docs/iam/fill-in-iam-user-info.png)

Select **Attach existing policies directly**.

![Add IAM User Policy Screenshot](/assets/docs/iam/add-iam-user-policy.png)

Search for **AdministratorAccess** and select the policy, then select **Next: Review**.

You can provide a more finely grained policy by following the instructions in the [Customizing your IAM Policy]({% link _docs/customizing-your-iam-policy.md %}) chapter.

![Added Admin Policy Screenshot](/assets/docs/iam/added-admin-policy.png)

Select **Create user**.

![Review IAM User Screenshot](/assets/docs/iam/review-iam-user.png)

Select **Show** to reveal **Secret access key**.

![Added IAM User Screenshot](/assets/docs/iam/added-iam-user.png)

Take a note of the **Access key ID** and **Secret access key**.

![IAM User Credentials Screenshot](/assets/docs/iam/iam-user-credentials.png)

Use these as the **IAM Access Key** and the **IAM Secret Key** when you [create your project]({{ site.console_url }}/new).
