---
layout: common-errors
title: Export resource cannot be deleted as it is in use
image: /assets/social-cards/common-errors.png
description: "An error occurred: xxxxx-xxxxx-xxxxx-xxxxx-dev - Export dev-xxxxx cannot be deleted as it is in use by xxxxx-xxxxx-xxxxx-xxxxx-dev."
---

#### Error Message

> An error occurred: xxxxx-xxxxx-xxxxx-xxxxx-dev - Export dev-xxxxx cannot be deleted as it is in use by xxxxx-xxxxx-xxxxx-xxxxx-dev.


#### Problem

Your CloudFormation stack is exporting a value that is being referenced by another stack. You can't modify or remove the value while it is in use.

This error usually happens while trying to remove services that depend on each other. They might have been deployed in a specific order. And so the services that are exporting a value need to be removed at the end.


#### Solution

The error message tells you which stack is referencing the exported value. Go to the corresponding service's `serverless.yml` and identify where you are importing the value. Remove the reference and deploy the updated service.

After the service has been successfully deployed, you can now act on the original service that was exporting the value.
