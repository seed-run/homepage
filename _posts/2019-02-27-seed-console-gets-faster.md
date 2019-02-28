---
layout: post
title: Seed Console Gets Faster
author: frank
---

The [Seed Console](https://console.seed.run) just got a whole lot faster. Seed is built completely on the [Serverless Stack](https://serverless-stack.com). We made a few changes to drastically improve the response times of the Lambdas that power our APIs.

![Before and after Lambda performance graph](/assets/blog/seed-console-gets-faster/before-and-after-lambda-performance-graph.png)

Using Lambda and API Gateway to power your APIs is a very common use case for Serverless applications. All of the APIs that we build at Seed are Serverless. However, the Lambda and API Gateway combination needs a little tuning to be performant.

Above, is a graph showing the response time for our most popular API endpoint. As you can see, it wasn't very fast before we made the performance improvements. So it's worth going over some of the changes we made. Note that, we are using [Serverless Framework](https://serverless.com), our Lambdas are in Node.js, and we use DynamoDB as our datastore. And the numbers above don't reflect cold-start times. We'll tackle that in a separate post.

1. **Individually packing functions**

   The first big change we made was reducing the size of our Lambdas. Previously, our Node.js Lambda functions were packed along with all the `node_modules/` and the same package was used for all the Lambda functions in a service. This meant that the compressed package size in many cases was nearly 50MB. To fix this, we first individually packaged all our [Lambda functions](https://serverless.com/framework/docs/providers/aws/guide/packaging#packaging-functions-separately). If you are not familiar with this option in Serverless Framework, it creates separate packages for each of your Lambda functions. This might slow down your deploys. But in combination with the next tip, can really reduce the size of your Lambda functions.

2. **Tree Shaking with Serverless Webpack**

   Next, we used [Serverless Webpack](https://www.github.com/serverless-heaven/serverless-webpack) to generate a single JS file per Lambda function. This takes advantage of [Webpack's Tree Shaking](https://webpack.js.org/guides/tree-shaking/) optimization. The result is that most of our Lambda functions are now 1-3 MB compressed. We'll be writing more about this in detail over on [Serverless Stack](https://serverless-stack.com) soon.

3. **Batch Gets with DynamoDB**

   Any complicated API typically ends up needing to make quite a few queries to compile the necessary data. By default we were making most of these queries sequentially. Even though DynamoDB is fast; this can still be a slow process, depending on the number of queries. We made a few different code changes to [batchGet our DynamoDB requests](https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS/DynamoDB/DocumentClient.html#batchGet-property). Effectively, making most of our requests concurrently.

4. **Enable HTTP keep-alive**

   Finally, we enabled HTTP keep-alive for our Node.js Lambda functions. You can read more about this [in detail over at Yan Cui's blog](https://theburningmonk.com/2019/02/lambda-optimization-tip-enable-http-keep-alive/). This flag matters a lot more when making short-lived calls, like the ones we make to DynamoDB.


And there you have it, a few simple optimizations resulting in a much faster [Seed Console](https://console.seed.run). We are in no way done yet but it's still worth sharing what we've learnt from our little optimizations. We decided from day 1 to be a Serverless first organization and we honestly cannot recommend it enough. With a few basic steps you can make sure your Serverless APIs are fast and performant. 
