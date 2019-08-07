---
layout: post
title: Should I use a hosted or on-premise CI/CD for my Serverless app?
image: assets/social-cards/serverless-cicd-tips.png
description: In this post we are going to compare hosted and on-premise CI/CD solutions for Serverless apps. We'll try and compare them across a few different criteria so you can decide what is best for your team.
categories: tips
author: frank
---

In this post we are going to compare hosted and on-premise CI/CD solutions for Serverless apps. We'll try and compare them across a few different criteria so you can decide what is best for your team.

Just to be clear, when we refer to hosted, we mean that a separate service provider is hosting the CI/CD pipeline. Whereas for the on-premise option, you are responsible for installing and managing the CI/CD software on your own infrastructure.

Let's start by comparing the two options when it comes to getting started.

### 1. Getting started

While getting started with hosted services are quicker; there is a learning curve when you first start using it. Most of your time is spent understanding the details of the hosted service. For the on-premise option, getting started is comparatively more complicated. You are involved in the initial setup process which includes installing it within your infrastructure.

For Serverless apps specifically, the learning curve can vary drastically for a service like [Seed](/) (that's on the simpler side), to Travis CI or CircleCI (which is more on the complicated side). This is primarily because you need to configure the pipelines yourself.

So if you want to skip the process of installing and maintaining the CI/CD infrastructure, choose the hosted option. And if you want to skip the process of maintaining your own pipelines, use a fully managed provider like Seed.

### 2. Cost

For on-premise options, the cost for your pipeline is simply your infrastructure cost. If you are on AWS, this is the EC2 cost to run your build machines. You can take advantage of the EC2 free tier to get started.

Hosted CI/CD services on the other hand require you to pay some sort of a monthly fee or are pay-per-use. Most of them do come with a generous free tier for you to get started. Seed is free for the first 500 minutes a month, which is more than enough if you are an individual developer or a small team.

Of course, the factor to consider when it comes to the on-premise options is the DevOps cost. If you imagine you have somebody on your team that is responsible for setting up the infrastructure and maintaining it. Note that for deploying Serverless applications, your DevOps person need to be someone that is familiar with the details of the AWS services that are used as a part of your stack. This can cause on-premise options to get fairly expensive. For small teams the responsibility of maintaining the CI/CD pipeline usually falls on the CTO or the tech lead. This isn't a good use of their time, especially in the early stages.

### 3. Infrastructural flexibility

For on-premise options, you have complete control over the underlying infrastructure. You can spin up your build machine with any vCPU, RAM, and disk space. On the other hand for hosted providers for example, CircleCI supports up to 16GB RAM and 8vCPU; and [Seed](/) supports up to 15GB RAM and 8vCPU.

This is usually not a concern while getting started, as 16GB and 8vCPU is more than enough for most projects. However, if you are a large enterprise and your build process involves some heavy-lifting, you might feel constrained by the hosted options.

### 4. Customizability

With on-premise options, you can create something to fit your exact needs, right down to the details of a specific machine. As your pipeline grows more complicated, you won't have to worry about out growing the feature set offered by the hosted service.

This is where the on-premise options really shine. That said the hosted options do give you ways to extend and integrate with other services. So it's worth looking into the specific provider you are considering.

### 5. Security

For on-premise options, the pipeline lives and run within your own infrastructure. You can easily secure and comply your company's security policy. Assuming that your security team has a good understanding of the CI/CD service you are using, you should be able to secure it to meet your needs.

With hosted services, you are reliant on the service provider for keeping your pipelines secure. This can be a concern if their policies are not in accordance with your company's policy. However, you need to weigh this against the expense of having your own security/DevOps person to manage your pipeline.

#### Conclusion

The key decision really comes down to you having the resources (a DevOps person or team) to manage the infrastructure and pipeline. If you are a small to medium sized team, definitely use a hosted service. The setup process is usually very quick, in fact it takes most teams less than 15 minutes to setup their pipeline and make their first deployment on Seed. There is minimal maintenance and you can get started for free.

On the other hand, if you have specific requirements for your pipeline, that could either be the infrastructure requirements or security compliance; go with the on-premise options. It gives you complete control over your pipeline.
