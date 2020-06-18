---
layout: common-errors
title: Function doesn't exist in this service
image: /assets/social-cards/common-errors.png
description: Function "xxxxxx" doesn't exist in this Service
---

#### Error Message

> Function "xxxxxx" doesn't exist in this Service


#### Problem

Serverless Framework is complaining that it cannot find a Lambda function with the specified name.


#### Solution

Here are a few things to check if you are running into this issue:

1. Double check the spelling and case. Ensure the name of the function you are trying to invoke matches the one defined in the functions section of your `serverless.yml`. For example, if your `serverless.yml` looks like:

   ``` yml
   service: hello-world
   
   ...
   
   functions:
     get:
       handler: get.main
   ```

   The correct function name when trying to invoke is `serverless invoke local -f get`, not `serverless invoke local -f hello-world-dev-get`.


2. Alternatively, if you are doing a remote invoke (not `serverless invoke local`), make sure the service has been successfully deployed. You can check if the service has been deployed by running `serverless info`. And the function you are trying to invoke should be listed under functions.

   For example, you might see something like this:

   ```
   Service Information
   service: hello-world
   stage: dev
   region: us-east-1
   stack: hello-world-dev
   resources: 11
   api keys:
     None
   endpoints:
     GET - https://xxxxxxxxxx.execute-api.us-east-1.amazonaws.com/dev
   functions:
     get: hello-world-dev-get
   layers:
     None
   ```

   This means that you can now invoke the function using `serverless invoke -f get`.
