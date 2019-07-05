---
layout: post
title: Deployment Info
categories: news
author: jay
---

Once you successfully deploy to a stage; Seed can display information on the deployment. 

![View Deployment](/assets/blog/deployment-info/deployment-info.png)

By heading over to the deployment page you can see a list of all the Lambdas and API Gateway endpoints. This gives you the ability to quickly view the resources that have been deployed to a specific stage.

This information could previously be access by [running the `serverless info` command](https://serverless.com/framework/docs/providers/aws/cli-reference/info/). However, if you have a large number of services deployed across multiple stages/environments; it can be hard to get a overview of the resources. By giving you a clear view of the stack, Seed makes it easy to manage and monitor your Serverless deployments.
