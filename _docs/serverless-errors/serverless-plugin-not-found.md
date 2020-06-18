---
layout: common-errors
title: Serverless plugin not found
image: /assets/social-cards/common-errors.png
description: Serverless plugin not found. Make sure it's installed and listed in the "plugins" section of your serverless config file.
---

#### Error Message

Depending on the plugin, you might see an error like this:

> Serverless plugin "serverless-webpack" not found. Make sure it's installed and listed in the "plugins" section of your serverless config file.


#### Problem

The plugin, in this case, `serverless-webpack` is listed under the `plugins` section in your `serverless.yml`, but the plugin is not installed.


#### Solution

Serverless Framework and all its plugins are in Node.js and are available as NPM packages.

To fix this error:

- Double check the name of the plugin.
- Ensure the plugin is installed correctly. In the case of `serverless-webpack`, use the `npm install --save-dev serverless-webpack`.
