---
layout: common-errors
title: Enabling API Gateway X-Ray Tracing for existing deployments requires a remove and re-deploy of your API Gateway
image: /assets/social-cards/common-errors.png
description: "NOTE: Enabling API Gateway X-Ray Tracing for existing deployments requires a remove and re-deploy of your API Gateway."
---

#### Error Message

> NOTE: Enabling API Gateway X-Ray Tracing for existing deployments requires a remove and re-deploy of your API Gateway.


#### Problem

Due to CloudFormation limitations it's not possible to enable AWS X-Ray Tracing on existing deployments.


#### Solution

The easiest way to enable X-Ray Tracing on existing deployments is to remove the old API Gateway project and re-deploy it with tracing enabled. However, by removing and re-deploying, the API endpoint will change.
