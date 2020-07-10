---
layout: docs
title: Issues and Alerts
---

**Issues** in [Seed](/) makes it very easy to monitor your Serverless app. Issues is a native, real-time Lambda monitoring and alerting service, that:

- Works out-of-the-box. No code changes or external SDKs needed.
- Sends Slack or email alerts with a complete log of the failed request.
- Autodetects all Lambda failures. Including out of memory and timeouts.
- Supports native error reporting. Use `console.error` to report any exceptions.

![Issues feed in Seed](/assets/docs/issues-and-alerts/issues-feed-in-seed.png)

Issues is currently in private beta. Head over to your app and join the waitlist. And we'll contact you once we are ready for you.

In this chapter here's what we'll be going over:

- [How it works](#how-it-works)
- [Enabling Issues](#enabling-issues)
  - [Default Stage](#default-stage)
- [Types of Lambda errors](#types-of-lambda-errors)
- [Native error reporting](#native-error-reporting)
- [Grouping errors](#grouping-errors)
- [Notifications](#notifications)
- [Ignoring or resolving issues](#ignoring-or-resolving-issues)
  - [Flag ignored issues](#flag-ignored-issues)
- [Automatically ignored issues](#automatically-ignored-issues)
- [Usage and limits](#usage-and-limits)
- [Additional IAM permissions](#additional-iam-permissions)

------

### How It Works

Issues works by subscribing to the CloudWatch log groups for all your Lambda functions. It'll listen for any errors and report them to the Seed console. And it'll optionally send you a Slack or an email notification.

Traditional error reporting services make HTTP calls to 3rd party servers to report errors. This slows down your Lambda functions as it has to wait for the reporting to complete before proceeding.

Since Issues is completely native, it doesn't need any code changes or external SDKs. This means that it does not impact your application performance in anyway. It simply reads the CloudWatch logs asynchronously and reports the errors.

And you get the complete request log, plus a link to X-Ray (if configured).

![Issues request logs](/assets/docs/issues-and-alerts/issues-request-logs.png)

Note that, the logs are loaded directly from CloudWatch. This means that if you have a short log retention period, the logs for some older issues might not load anymore. It is recommended that you set your CloudWatch log retention period to at least 30 days, to match how long [the issues are available for](#usage-and-limits).

### Enabling Issues

Once enabled, Issues will subscribe to the CloudWatch log groups for your Lambda functions. And it'll keep it updated when you deploy your services. Finally, it'll remove these subscriptions when you remove your app or disable Issues.

Head over to your app settings > Manage Issues > and hit **Enable Issues**.

![Enable issues in app settings](/assets/docs/issues-and-alerts/enable-issues-in-app-settings.png)

This process can take a few minutes.

![Enable issues in progress](/assets/docs/issues-and-alerts/enable-issues-in-progress.png)

Note that, CloudWatch log groups can only have 1 subscriber. This means that if you are currently using another monitoring service, you'll get an error while trying to enable it. To fix this you'll need to enabled the **Use Seed to exclusively subscribe to all Lambda functions** option.

![Enable issues with exclusive flag](/assets/docs/issues-and-alerts/enable-issues-with-exclusive-flag.png)

This setting tells Seed to remove any existing subscriptions before enabling Issues. You can also optionally select a stage that you want to enable it for. This will allow you to try out Issues without having to remove the existing subscriptions from your production environment.

If you are looking for a way to setup Issues while still keeping your existing subscriptions, [get in touch with us](mailto:{{ site.email }}). 

#### Default Stage

Issues is enabled for all the stages in your app. But it defaults to showing you your _production_ stage first. So if you click on the Issues tab in your app, you'll be shown the issues from your _production_ stage.

However, you might have multiple production stages or you might have not deployed to production yet. In these cases you can change the default stage that's used. To do this, head over to the Issues settings.

![Default stage Issues setting](/assets/docs/issues-and-alerts/default-stage-issues-setting.png)

And select the stage you want.

Note that, this setting has no impact on how the stages are monitored. It simply allows you to view the specified stage by default.

### Types of Lambda Errors

Issues will autodetect all Lambda errors including:

- Timeouts
- Out of memory errors
- Lambda failures (any unhandled exceptions)

### Native Error Reporting

While unhandled errors are automatically reported to Issues. The errors and exceptions that you are catching in your code need to be manually reported. Issues allows you to do this natively. Without having to install any 3rd party SDKs or libraries. Simply log it as an error to the console!

You can [read more about native error reporting here]({% link _docs/native-error-reporting.md %}).

### Grouping Errors

Errors are grouped together using the following algorithm:

1. First if the stack trace is available, each stack trace frame is normalized and grouped by:
  - Module name
  - Normalized filename (with revision, hashes, etc. removed)
  - Normalized context line (a cleaned up version of the source code of the affected line, if provided)
2. If stack trace is not available, but exception info is, it's grouped by exception code and message.
3. If the error is not an exception, ie. `console.error('my message')`, it's group by message.

### Notifications

You can configure Issues to alert you of an error by sending you a notification (via Slack or email). Head over to your Issues settings to set this up.

![Configure notifications for issues in Issues settings](/assets/docs/issues-and-alerts/configure-notifications-for-issues-in-issues-settings.png)

Once configured, you'll receieve alerts in Slack when an error is detected.

![Issues Slack alert](/assets/docs/issues-and-alerts/issues-slack-alert.jpg)
*Issues Slack alert*

Note that, you will not be notified again by the same Issue (groups of similar errors) in 30 minutes. And for emails, you won't receive more than one in a 10 minute span.

### Ignoring or Resolving Issues

You might have fixed an error and would like to resolve the issue on Seed. Or you might want to ignore certain errors. You can do so from the issue page.

![Ignore or Resolve in the Issue page](/assets/docs/issues-and-alerts/ignore-or-resolve-in-the-issue-page.png)

When an issue is ignored, you will not get notified about it or about any errors that might be grouped together with it. Ignored issues are also hidden in the feed by default.

On the other hand, When an issue is marked as resolved; it will not show up in the Issues feed. If it happens again, it will re-appear in your feed. And you will get notified immediately.

![View ignored and resolved Issues](/assets/docs/issues-and-alerts/view-ignored-and-resolved-issues.png)

Note that, you can choose to view all ignored and resolved issues on your feed by hitting the switch on the top right.

#### Flag Ignored Issues

If you find yourself ignoring the same error too many times, you can flag it.

![Flag ignored Issues](/assets/docs/issues-and-alerts/flag-ignored-issues.png)

We'll have a look at the flagged error and add it to our list of automatically ignored issues.

### Automatically Ignored Issues

Issues uses the standard console logger to detect errors. However, some libraries or packages log warnings or messages incorrectly as errors. These get reported to Issues and can drown out the real errors in your application.

So some of these issues that are automatically ignored. Currently, all `DeprecationWarning` errors in Node.js are automatically ignored. You can read more about these errors over on the [common Serverless errors page]({% link _docs/serverless-errors/deprecationwarning.md %}).

You can unignore these errors. Or if you think an error is being ignored by mistake, [feel free to let us know](mailto:{{ site.email }}).

### Usage and Limits

Issues is free for all users on Seed. But there are some soft limits to prevent accidental overuse.

- Maximum of 10K errors per hour
- Error related data is retained for 30 days

If these limits don't work for you or if you have any questions, [feel free to contact us](mailto:{{ site.email }}).

### Additional IAM Permissions

To connect to your AWS account and monitor errors, Seed needs the following set of additional permissions.

``` javascript
{
  "Sid": "ManageIssues",
  "Effect": "Allow",
  "Action": [
    // Read permission: Get log groups in a deployed stack
    "cloudformation:ListStackResources",
    // Read permission: Get deployed stack information
    "cloudformation:DescribeStacks",
    // Read permission: Check existing log group subscription
    "logs:DescribeSubscriptionFilters",
    // Write permission: Add log group subscription to enable Issues
    "logs:PutSubscriptionFilter",
    // Write permission: Remove log group subscription when disabling Issues
    "logs:DeleteSubscriptionFilter",
    // Read permission: Check Lambda runtime
    "lambda:GetFunction"
  ],
  "Resource": "*"
}
```

Issues makes it really easy to monitor the errors in your Serverless app in real-time. All without having to make any changes to your code or without the use of 3rd party SDKs.
