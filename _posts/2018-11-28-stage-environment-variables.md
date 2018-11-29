---
layout: post
title: Stage Environment Variables
author: jack
---

We recently rolled out a simple but highly requested feature; the ability to configure environment variables across all your services.

Previously, you had to configure environment variables for each and every service in a stage. For some of us that have Serverless applications that contains dozens of services, this can be a major hassle.

We've now made it so that you can simply set your secrets or environment variables for a stage and they will be applied to all the services in that stage.

You can read more about [storing secrets in our docs]({% link _docs/storing-secrets.md %}). 
