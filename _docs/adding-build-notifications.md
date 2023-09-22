---
layout: docs
title: Adding Build Notifications
---

Seed makes it easy to configure your stages with email, slack, and custom webhook notifications. Notifications are sent when a build is deployed to a stage.

You can configure each stage separately. For example, maybe you only want to be notified for updates to the production stage. Or maybe you want a specific stage to notify a specific member on your team.

To add build notifications, head over to your app settings and select the stage under **Stage Settings** on the right.

![Select stage](/assets/docs/adding-build-notifications/select-stage.png)

Select **Show Notification Options**.

![Click Show Notification Options](/assets/docs/adding-build-notifications/click-show-notification-options.png)

Note that, you'll be notified for all services that are built in this stage.

### Notification Options

By default, you'll be notified for all the build events (success and failure).

![Notification events](/assets/docs/adding-build-notifications/notification-events.png)

You can change this to only be notified for failed builds by clicking on the dropdown and selecting **Build failures** as the **Notification event**.

![Notification build failure event](/assets/docs/adding-build-notifications/notification-build-failure-event.png)

The **Notification type** allows you to pick the way you want to be notified. Seed can notify you via email, Slack, or a custom webhook.

### Email Notifications

Add the email of the person you'd like to notify from the stage settings.

![Add email notification](/assets/docs/adding-build-notifications/add-email-notification.png)

You'll receive email notifications for successful and failed deployments.

### Slack Notifications

To configure your Slack you need to:

1. Create an **Incoming Webhook**. You can follow this [simple guide to configure an Incoming Webhook](https://get.slack.help/hc/en-us/articles/115005265063-Incoming-WebHooks-for-Slack).

2. Add the webhook URL and the slack channel you'd like to send the notifications to. The channel is optional, since the webhook comes configured with a default channel.

![Add slack notification](/assets/docs/adding-build-notifications/add-slack-notification.png)

You'll receive slack notifications for when a build is starting and if it succeeds or fails.

### Custom Webhooks

To configure your webhook to be notified you can specify the **Webhook URL**. And optionally, you can pass in a **JWS secret token**.

![Add webhook notification](/assets/docs/adding-build-notifications/add-webhook-notification.png)

If the JWS secret token is provided, Seed will generate a JSON Web Signature and pass it as the `x-webhook-signature` in the request header.

And here is an example of the Webhook request body.

``` json
{
  "status": "deploying",
  "app_id": "6253a1978af24a12973a5049f161f348",
  "app_link": "https://console.seed.run/seaboard/seaboard-backend-v2",
  "stage_id": "dev",
  "stage_link": "https://console.seed.run/seaboard/seaboard-backend-v2/stages/dev",
  "build_id": 227,
  "build_link": "https://console.seed.run/seaboard/seaboard-backend-v2/activity/stages/dev/builds/227",
  "ts": 1693997084.315
}
```

Where the `status` field can be either `deploying`, `success`, or `failure`.
