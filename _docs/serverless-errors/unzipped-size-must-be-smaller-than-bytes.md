---
layout: build-errors
title: Unzipped size must be smaller than xxxx bytes
image: /assets/social-cards/common-errors.png
description: "An error occurred: LambdaFunction - Unzipped size must be smaller than 262144000 bytes (Service: AWSLambdaInternal; Status Code: 400; Error Code: InvalidParameterValueException; Request ID: xxxx-xxxx-xxxx-xxxx)."
---

#### Error Message

> An error occurred: LambdaFunction - Unzipped size must be smaller than 262144000 bytes (Service: AWSLambdaInternal; Status Code: 400; Error Code: InvalidParameterValueException; Request ID: xxxx-xxxx-xxxx-xxxx).


#### Problem

There is a limit of 250MB on the size of your Lambda function after it has been unzipped. Recall that, your Lambda functions are packaged as zip files and sent to AWS. Once AWS unzips them, the entire directory needs to be smaller than 250MB.

You can read more about the [AWS Lambda limits here](https://docs.aws.amazon.com/lambda/latest/dg/limits.html).


#### Solution

The fix here is pretty obvious. Try and reduce the size of the Lambda function package.

There are a couple of simple ways to do this:

- If your Lambda is in Node.js; using [serverless-webpack](https://www.github.com/serverless-heaven/serverless-webpack) can significantly reduce the size.
- Package the Lambda functions individually using the `individually: true` flag. You can read more about this [in the Serverless Framework docs](https://serverless.com/framework/docs/providers/aws/guide/packaging/).
- If you have large binaries, images, or files as a part of the package; store them on S3 and download them runtime.

Remember that large Lambda function code size can negatively impact cold start times. So in general it's a good idea to keep your Lambdas small.
