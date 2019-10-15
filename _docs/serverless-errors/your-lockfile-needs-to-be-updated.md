---
layout: build-errors
title: Your lockfile needs to be updated
image: /assets/social-cards/common-errors.png
description: "yarn install --frozen-lockfile --non-interactive failed with code 1. error Your lockfile needs to be updated, but yarn was run with `--frozen-lockfile`."
---

#### Error Message

> yarn install --frozen-lockfile --non-interactive failed with code 1

> error Your lockfile needs to be updated, but yarn was run with `--frozen-lockfile`.


#### Problem

This error is caused by [serverless-webpack](https://github.com/serverless-heaven/serverless-webpack) when trying to deploy your app using the `serverless deploy` or `serverless pacakge` command.

This is happening because serverless-webpack is trying to build your app and the Yarn lockfile that it generates is not the same as the one you have in your repo.

#### Solution

Make sure that:

1. The packages in your `package.json` have a version specified. If you have an empty version (`""`), the generated version might be different from the one in your lockfile.

2. You might be referencing a package in your Lambda function that has not be specified in your `package.json`.
