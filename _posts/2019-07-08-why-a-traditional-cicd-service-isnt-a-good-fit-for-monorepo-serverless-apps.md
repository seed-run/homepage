---
layout: post
title: Why a traditional CI/CD service isn't a good fit for monorepo Serverless apps?
image: assets/social-cards/serverless-cicd-tips.png
description: You might have come across the idea that if you are deploying a Serverless app, your build servers should be Serverless as well. In this post, we are going to dive into this idea and explore why a traditional CI/CD service (like CircleCI or Travis CI) isn’t a good fit for deploying monorepo Serverless apps.
categories: tips
author: frank
---

You might have come across the idea that if you are deploying a Serverless app, your build servers should be Serverless as well. In this post, we are going to dive into this idea and explore why a traditional CI/CD service (like [CircleCI](https://circleci.com) or [Travis CI](https://travis-ci.com)) isn't a good fit for deploying monorepo Serverless apps.

### Background

Let's first look at how a monorepo Serverless app is different from a traditional monolithic app:

1. App structure

   A monorepo app is made  up of a collection of services. These services are loosely coupled, independently testable, and also independently deployable. A monolithic app on the other hand is a single large application, (like a Rails or Express app).

2. Tests

   Each service comes with its own unit tests that that are ideally side-effect free. This means that the tests can be run independently (or concurrently). On the other hand a monolithic app usually has a single test suite for the entire application.

3. Deployments

   Each service can be deployed completely independently. And not all services need to be deployed on each Git push. You might want to only deploy the services that have changed.

### Deploying monorepo apps

Now let's see how this architectural shift changes our CI/CD pipeline.

Traditional CI/CD services give you an instance that's available to you 24/7 to run your pipeline. Think of it like an EC2 instance with the pipeline application preloaded on it. On git push, your build instance pulls the code from Git, runs some tests, packages your code and deploys it. This works great for monolithic app since you are testing your application and deploying it as a whole.

With a Serverless app on the other hand, you test and deploy each service independently. Also, you'd want to do this concurrently to speed up the build/test process. This poses a challenge. If you have to deploy two services, and you want to deploy them concurrently, you would need to pay to keep two build servers. The cost in this case scales with the number of services you want to deploy concurrently. This forces you to either deploy your services sequentially (having a slow pipeline); or to deploy them all in parallel and pay a large bill.

Additionally, you might not want to deploy all your services on every single commit. This makes it tricky to utilize your build resources efficiently.

Ideally, you'd want your CI/CD service to be Serverless as well! That way you can use the exact amount of resources necessary for a build process. Instead of having to keep all the build servers always running. You'd want to use a micro-service friendly CI/CD provider that facilitates bursts of highly concurrent deployments. [Seed](/) and [AWS CodeBuild](https://aws.amazon.com/codebuild/) are two such services. Your cost scales with the amount of build minutes you use, so it's resource efficient. And you essentially have unlimited concurrency, meaning your builds will always be fast!
