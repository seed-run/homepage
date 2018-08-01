---
layout: post
title: Pretty Printed Logs
image: /assets/social-cards/pretty-printed-logs.png
author: aash
---

Lambda logs in Seed are now pretty printed when displaying JSON objects.

![Pretty printed JSON Lambda logs](/assets/blog/pretty-printed-logs/json-lambda-logs.png)

Now you can use Seed's real-time logs to better debug your Lambda functions. Any JSON stringified object printed using `console.log` will get pretty printed. So for example adding the following, will give a pretty printed version of the [context object in your Lambda function](https://docs.aws.amazon.com/lambda/latest/dg/nodejs-prog-model-context.html).

``` javascript
console.log(JSON.stringify(context));
```

[Real-time Lambda and API Gateway logs]({% link _docs/viewing-logs.md %}) allow you to easily monitor your Serverless deployments in Seed.
