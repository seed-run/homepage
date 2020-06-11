---
layout: post
title: Issues Beta
categories: news
author: frank
---

If you've checked out the [recent Seed console redesign]({% link _posts/2020-06-10-seed-console-gets-a-ux-update.md %}), you might have noticed a new tab in your apps. **Issues** — native, real-time Lambda monitoring and alerting.

![Issues feed in Seed](/assets/blog/issues-beta/issues-feed-in-seed.png)

Issues is currently in private beta. We've been using it internally for sometime now and it:

- Works out-of-the-box. No code changes or external SDKs needed.
- Sends Slack or email alerts with a complete log of the failed request.
- Autodetects all Lambda failures. Including out of memory and timeouts.
- Supports native error reporting. Use `console.error` to report any exceptions.

![Issues details page in Seed](/assets/blog/issues-beta/issues-details-page-in-seed.png)

Issues is free during the beta. And thanks to our smart log subscription algorithm, it'll be a lot more cost-effective than comparable offerings!

We'll be releasing more details about Issues in the coming weeks as we prepare for a public launch. In the meantime, [check out our docs on it]({% link _docs/issues-and-alerts.md %}).

#### Joining the Beta

If you'd like to be a part of the beta, head over to your app and click **Join Waitlist** to reserve your place in line. We'll send you an invite once we are ready to enable it for your account! 
