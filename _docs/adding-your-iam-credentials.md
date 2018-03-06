---
layout: docs
title: Adding your IAM Credentials
---

[Seed](/) needs your AWS IAM credentials to deploy your project on your behalf to your AWS account. There are two ways to get your credentials.

### 1. Your Existing Credentials

This is the quickest way to get your IAM credentials. If you have run the `serverless deploy` command in your terminal; you have probably configured your AWS CLI. And the IAM credentials are stored in `~/.aws/credentials`. By running the following:

``` bash
$ cat ~/.aws/credentials
```

The format of this looks something like this:

```
[default]
aws_access_key_id = AKABCDEFGHIJ72LMNOPQ
aws_secret_access_key = 7r0uzfABCDefgh11234567ijklmnop09875quwzs
```

Here the `aws_access_key_id` is your **IAM Access Key** and `aws_secret_access_key` is your **IAM Secret Key**.

While it is easy to get your existing credentials, it is better to create it from scratch. This gives you better control over what permissions are granted to Seed.

### 2. Create New Credentials

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

Here you can hit **Create policy** to provide a custom IAM policy based on the permissions your project needs. You can do this by following the instructions in the [Customizing your IAM Policy]({% link _docs/customizing-your-iam-policy.md %}) chapter.

But if you are just looking for a quick way to test your project on Seed you can search for **AdministratorAccess** and select the policy, then select **Next: Review**.

![Added Admin Policy Screenshot](/assets/docs/iam/added-admin-policy.png)

Select **Create user**.

![Review IAM User Screenshot](/assets/docs/iam/review-iam-user.png)

Select **Show** to reveal **Secret access key**.

![Added IAM User Screenshot](/assets/docs/iam/added-iam-user.png)

Take a note of the **Access key ID** and **Secret access key**.

![IAM User Credentials Screenshot](/assets/docs/iam/iam-user-credentials.png)

Use these as the **IAM Access Key** and the **IAM Secret Key** when you [create your project]({{ site.console_url }}/new).
