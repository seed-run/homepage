---
layout: post
title: Review Change Sets
categories: news
author: frank
---

You can now review your [AWS CloudFormation Change Sets](https://aws.amazon.com/blogs/aws/new-change-sets-for-aws-cloudformation/) when promoting to production in Seed. Change Sets are generated automatically when promoting a build to the production stage.

![Confirm Change Set](/assets/blog/review-change-sets/confirm-change-set.png)

A Change Set is generated as a part of the CI process by comparing the proposed changes in the build you are trying to promote to the current state of the production stage. The Change Set shows you the resources that are about to be *removed*, *added*, and *modified*. This means you get an accurate view of what is about to be changed.

Reviewing Change Sets is just one way Seed can help you manage your CI/CD pipeline for Serverless. You can [read more about promoting to production in our docs]({% link _docs/promoting-to-production.md %}).
