---
layout: post
title: Real-Time Lambda Monitoring in Seed
categories: news
author: frank
image: assets/social-cards/real-time-lambda-monitoring.png
tweet: https://twitter.com/SEED_run/status/1278671941759574016
---

Real-time Lambda monitoring and alerting is now available for all apps in Seed. You can find it in the _Issues_ tab in your console. Oh and we have a small surprise for you below.

![Issues feed in Seed](/assets/blog/real-time-lambda-monitoring-in-seed/issues-feed-in-seed.png)

Issues was [launched in private beta a couple of weeks ago]({% link _posts/2020-06-10-issues-beta.md %}). And during that time many of you have had a chance to use it in your production environments.

If you haven't had a chance to try it yet, here's a quick recap:

- Works out-of-the-box. No code changes or external SDKs needed.
- Sends Slack or email alerts with a complete log of the failed request.
- Autodetects all Lambda failures. Including out of memory and timeouts.
- Supports native error reporting. Use `console.error` to report any exceptions.

Let's dive into the details.

#### Nothing to install

You don't need to install any 3rd party SDKs, libraries, layers, or packages. Issues works completely **out of the box**.

![Enable Issues setting in Seed](/assets/blog/real-time-lambda-monitoring-in-seed/enable-issues-setting-in-seed.png)

If you are setting up a new app on Seed, it'll be automatically enabled. If not, you can head over to your app settings and turn it on.

#### Autodetect all Lambda failures

Unlike other error reporting services, Issues will **catch all Lambda failures**. This includes out of memory errors, timeouts, etc.

#### Native Error Reporting

For cases where you want to report an error or exception in your code. Simply, `console.error(e)`. We call this [Native Error Reporting]({% link _docs/native-error-reporting.md %}).

It has a couple of key advantages:

1. You don't need to **make any code changes**. Just log the error to the console and it'll get reported.
2. There is **no impact on performance**. Other services need your Lambda functions to wait for the error to be reported via a 3rd party HTTP call. This can slow your functions down.

So that means you can do this in your Lambda function:

<p style="margin: 0 auto; text-align: center;">
  <img src="/assets/blog/real-time-lambda-monitoring-in-seed/lambda-function-with-console-error.png" alt="Lambda function with console.error" width="700" />
</p>

And if your users run into an exception, you'll get an alert with this:

![Issue details page in Seed](/assets/blog/real-time-lambda-monitoring-in-seed/issue-details-page-in-seed.png)

Also, any other `console.log` outputs show up in the request logs.

![Request log in Issue details page](/assets/blog/real-time-lambda-monitoring-in-seed/request-log-in-issue-details-page.png)

Currently, Native Error Reporting is supported in Node.js and Python. With support for other runtimes coming soon.

#### Slack and Email Notifications

You can setup Slack and email notifications when you get an error. Head over to your app settings to set this up.

![Issues notifications setting in Seed](/assets/blog/real-time-lambda-monitoring-in-seed/issues-notifications-setting-in-seed.png)

You can also set it up to be notified when an error happens in a specific stage.

### Pricing

Issues was free during the private beta. And we've got some awesome news to share. It'll be **completely FREE** for everybody!

So it doesn't matter if you are a startup about to launch your product or if you receive millions of requests a day, it'll be free for you!

We think real-time Lambda monitoring is essential to building a Serverless app. Without it, you are left completely in the dark. And it just doesn't make sense to pay hundreds or thousands of dollars for something that is an absolute necessity.

Note that, we do have some soft limits in place to prevent abuse or accidental overuse. You can [read more about it in our docs]({% link _docs/issues-and-alerts.md %}#usage-and-limits) and [feel free to get in touch](mailto:{{ site.email }}) if you have any questions.

### Thanks

A big thanks to everybody that took part in our private beta and provided us with some really valuable feedback.

Including Ricardo from [Avec](https://avec.app), who had some kind words for us:

> The real-time Lambda monitoring in Seed helped us to remove additional paid third-party monitoring tools that add more workload, cost and latency in our functions. It's amazing that it's all centralized in the same service that deploys all our applications. And it really helps us to debug and fix issues in all environments.

Reiner from [The Core Group](http://coreltd.com/):

> The real-time Lambda monitoring in Seed makes it really easy for us to debug and fix issues in production. The ability to console.error to report issues is prompting me to rethink how we log and handle errors, in a good way!

And Patryk from [Tale Commerce](https://www.talecommerce.pl):

> I'm in the process of scaling my microservices and the Issues feature saved me a lot of headache. Having everything in one spot is really handy. I'm also glad that I don't have to pass my users data to another company. I've been with Seed for almost a year and I love the service!

-------

At [Seed](/), we want to make sure that your team has the best possible Serverless development experience. If you haven't tried Seed yet, here is what it can help you with:

- Manage your environments
- Git push to deploy with zero-configuration
- And send you real-time error alerts for your Lambda functions!

We are really excited to be able to build out the entire workflow. And to make it as easily accessible as possible for everybody!
