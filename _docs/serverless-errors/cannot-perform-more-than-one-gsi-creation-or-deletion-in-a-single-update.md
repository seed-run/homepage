---
layout: common-errors
title: Cannot perform more than one GSI creation or deletion in a single update
image: /assets/social-cards/common-errors.png
description: Cannot perform more than one GSI creation or deletion in a single update.
---

#### Error Message

> Cannot perform more than one GSI creation or deletion in a single update.


#### Problem

This error occurs when you try to:

- create a DynamoDB table with more than one Global Secondary Index (GSI); or
- add or remove more than one GSI for an existing table

This implies that you can only perform one GSI creation/deletion for a given table per  `serverless deploy`.


#### Solution

A work around would be to break up your changes to only perform one GSI update at a time.

For example, if you need to add a GSI and also remove one in a table, try the following:

1. Add the first GSI and run `serverless deploy`
2. Wait for the GSI to be created and for it to show an `Active` status
3. Remove the second GSI and run `serverless deploy` again

Note that, the second step can take longer for existing tables with large number of rows, as DynamoDB backfills the index.
