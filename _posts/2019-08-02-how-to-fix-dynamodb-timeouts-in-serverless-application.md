---
layout: post
title: How to fix DynamoDB timeouts in Serverless apps
image: assets/social-cards/dynamodb-timeout.png
description: In this post we are going to look at how to debug DynamoDB timeouts in Serverless apps. We are going to tweak the http connection timeout and the number of retries that the AWS SDK uses.
categories: tips
author: frank
---

In this post we are going to look at how to debug DynamoDB timeouts in Serverless apps. This is a fairly specific issue related to Node.js Lambda functions calling DynamoDB. But we recently had to work through this issue. Hopefully sharing our experience ends up being helpful to other folks.

Let's start by looking at the issue itself.

### The issue

We noticed that a certain percentage of our Node.js Lambda function calls were timing out. We used [AWS X-Ray to trace the calls]({% link _posts/2019-07-11-how-to-trace-serverless-apps-with-aws-x-ray.md %}) and found that the DynamoDB call seemed to be taking abnormally long. However there were no specific types of calls that were timing out. We observed timeouts across BatchGet, Get, Query, and Update calls.

Roughly 0.00002% of all our DynamoDB calls were timing out. We confirmed with [Mike Apted](https://twitter.com/mikeapted) that this is a farily normal timeout rate for DynamoDB calls.

Thus, the next step was to figure out how to handle these timeouts so that our users weren't being adversely affected by them.

There are two common ways DynamoDB calls might timeout.

### 1. HTTP connections are timing out

The first reason DynamoDB calls are taking long is because the HTTP requests that the AWS SDK is making to DynamoDB is timing out.

The AWS Node.js SDK has 2 settings:

1. HTTP Connect Timeout

   This sets the socket to timeout after failing to establish a connection with the server after a set amount of milliseconds. This timeout has no effect once a socket connection has been established.

2. HTTP Timeout

   Sets the socket to timeout after a set amount of inactivity on the socket. Defaults to two minutes.

On the other hand, for Lambda and API Gateway:
  - API Gateway has a maximum timeout setting of 29 sec.
  - Hence, Lambda should have a timeout of lesser than 29 sec.

And it only makes sense that DynamoDB's connection timeout is set to be lesser than that of Lambda. In fact, we **want to keep it short**. If DynamoDB times out, we want it to fail quickly and retry again. We want the DynamoDB calls to timeout before Lambda and API Gateway timeout. However, that is not what happens by default. As we talked about the issue above, our Lambda functions were timing out because the DynamoDB calls were taking too long.

So the first thing we need to do is to change the connection timeout for our DynamoDB client.

In our Lambda function, change the timeout by using the following:

``` js
import AWS from 'aws-sdk';

const dynamoDb = new AWS.DynamoDB.DocumentClient({
  httpOptions: {
    timeout: 5000
  }
});
```

### 2. Retries are taking long

Sometimes a DynamoDB call might fail. However, the response usually specifies if the error can be retried. By default, the AWS Node.js SDK client auto-retries such errors. It uses an exponential backoff strategy while retrying. For calls to most AWS services, the client auto-retries up to 3 times. It waits 100 ms before the first retry, 200 ms before the second, and 400 ms before the third attempt.

However for calls to DynamoDB, the client auto-retries up to 10 times. Starting with 50 ms for the first retry, then 100 ms, 200 ms, 400 ms all the way to 25600 ms for the last retry. The worst case scenario here is that a failed DynamoDB call takes over 50 sec before responding to your Lambda function. Given that API Gateway will timeout by 29 sec, you won't get to find out if the DynamoDB call timed out or errored out.

Hence, to be able to debug the issue, we **need to reduce the retry count** for our DynamoDB client. It needs to completely fail before our Lambda (or API Gateway) times out. 

To reduce the number of retries do the following:

``` js
import AWS from 'aws-sdk';

const dynamoDb = new AWS.DynamoDB.DocumentClient({
  maxRetries: 3
});
```

Now you should be able to figure out why your DynamoDB calls were failing in the first place.

#### Summary

Hopefully this post gives you a good idea on how to work with the DynamoDB timeouts that you are seeing in your Serverless app. A special thanks to [Mike Apted](https://twitter.com/mikeapted), [Adriano Raiano](https://twitter.com/adrirai), and [Carl Nordenfelt](https://twitter.com/carl_nordenfelt) for helping us track down the issue.
