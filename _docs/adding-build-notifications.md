---
layout: docs
title: Adding Build Notifications
---

Seed makes it easy to configure your stages with email, slack, and custom webhook notifications. Notifications are sent when a build is deployed to a stage.

You can configure each stage separately. For example, maybe you only want to be notified for updates to the production stage. Or maybe you want a specific stage to notify a specific member on your team.

To add build notifications, first select the service.

![Select service](/assets/docs/adding-build-notifications/select-service.png)

And select the stage.

![Select service stage](/assets/docs/adding-build-notifications/select-service-stage.png)

And from the **Settings**, select **Show Notification Options**.

![Select service stage settings](/assets/docs/adding-build-notifications/select-service-stage-settings.png)

### Email Notifications

Simply add the email of the person you'd like to notify from the stage settings.

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
  "build": 5,
  "stage": "dev",
  "service": "main",
  "status": "deploying",
  "commit": "5ad6f2d7b44ad77e5cfe925e7c9550b3be36c158",
  "service_link": "https://console.seed.run/apps/hello-world/services/default",
  "stage_link": "https://console.seed.run/apps/hello-world/services/default/stages/dev",
  "build_link": "https://console.seed.run/apps/hello-world/services/default/stages/dev/builds/5",
  "commit_link": "https://github.com/jayair/hello-world/commits/5ad6f2d7b44ad77e5cfe925e7c9550b3be36c158",
  "ts": 1530079736
}
```

Where the `status` field can be either `deploying`, `success`, or `failure`.
