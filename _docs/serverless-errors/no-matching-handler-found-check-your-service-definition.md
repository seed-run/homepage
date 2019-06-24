---
layout: build-errors
title: No matching handler found. Check your service definition.
image: /assets/social-cards/common-errors.png
description: No matching handler found for 'xxxx/xxxxxx' in '/xxxx/xxxx/xxxxxx'. Check your service definition.
---

#### Error Message

> No matching handler found for 'xxxx/xxxxxx' in '/xxxx/xxxx/xxxxxx'. Check your service definition.


#### Problem

This happens when Serverless Framework cannot find the handler file in the location specified in your `serverless.yml`.


#### Solution

Check to make sure that the path of the handler file matches the specified location.

Make sure to check the case of the handler paths. This error can occur if your OS or environment is case insensitive (like macOS), while the build server is case sensitive.

To fix this, you might need to delete the file and re-add it with the correct case. Simply renaming the file in macOS will not work.
