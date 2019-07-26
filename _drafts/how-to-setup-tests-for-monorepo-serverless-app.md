---
layout: post
title: How to setup tests for monorepo Serverless app?
image: 
description: 
categories: tips
author: jack
---

With Serverless, you are deploying both Code and Infrastructure. Infrastructure changes are not always (easily) reversible. Need to be extra careful releasing changes to production.

## Local Tests during development
  - Invoke Lambda functions locally via `sls invoke local` - https://serverless.com/framework/docs/providers/aws/cli-reference/invoke-local/
  - Invoke API Gateway endpoint locally using the 'serverless-offline' plugiin
## Test Lambda functions in each service before deploying
  - You can use the same testing frameworks you normally use. For Node, Mocha and Jest work just fine.
  - Lambda code usually interact with other AWS services. Mock the AWS SDK to ensure your test does not depend on them.
## Test overall app after all services are deployed
  - This can be integration tests / end-to-end tests / user acceptance tests for you
  - For API backends, tests are usually run against the API endpoint
  - Serverless applications ususally involve multiple AWS services. To ensure the AWS services' behaviours, you should not mock them in the overall test.
  - Because it is free (Lambda, API Gateway, DynamoDB) and easy (infrastructure as code) to replicating a stack at scale, you can have test environments mirroring the production.
  - Take advantage of AWS services
    - You can even setup many test environments and run test suites in parallel
    - Using DynamoDB's Backup Feature to snapshot the db and restore it to multiple test environments. (This works for test environments in the same AWS account)
## UI Tests
  - This is beyond the scope of the Serverless app, your can use Selenium or whatever tool u normally use. UI tests have not changed with serverless.
