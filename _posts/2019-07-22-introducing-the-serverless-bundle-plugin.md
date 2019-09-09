---
layout: post
title: Introducing the serverles-bundle plugin
image: assets/social-cards/serverless-bundle.png
description: Today we are open-sourcing a key part of the internal development workflow here at Seed. The serverless-bundle plugin is a zero-config way to generate optimized packages for your Node.js Lambda functions.
categories: community
author: jay
---

Today we are open-sourcing a key part of the internal development workflow here at [Seed](/). The [serverless-bundle](https://github.com/AnomalyInnovations/serverless-bundle) plugin is a zero-config way to generate optimized packages for your Node.js Lambda functions.

![serverless-bundle plugin npm screenshot](/assets/blog/introducing-the-serverless-bundle-plugin/serverless-bundle-plugin-npm-screenshot.png)

The serverless-bundle plugin is an extension of the amazing [serverless-webpack](https://github.com/serverless-heaven/serverless-webpack) plugin and is inspired by [Create React App](https://www.github.com/facebook/create-react-app).

### Background

Smaller Lambda function packages have lower cold start times. You can do this for your Serverless apps by packaging functions individually and using Webpack's tree shaking algorithm to only package the code your function needs.

Additionally, as JavaScript developers we'd like to use a similar syntax on both the client and the Lambda functions. We also want to be able to lint our code while developing. To do all of these things, you end up needing to install a whole slew of packages and plugins. And you have to manage all their configs.

```
"eslint"
"webpack"
"@babel/core"
"babel-eslint"
"babel-loader"
"eslint-loader"
"@babel/runtime"
"@babel/preset-env"
"serverless-webpack"
"source-map-support"
"webpack-node-externals"
"eslint-config-strongloop"
"@babel/plugin-transform-runtime"
"babel-plugin-source-map-support"
```

This can turn into a huge pain point when you are working on multiple Serverless apps. Especially when these packages need to be updated or maintained. For example, we wanted to speed up our build times and to do this the Webpack config needed to be updated. However, updating all of our projects with a list of config changes is a painful process. We've also faced this issue with our readers over on [Serverless-Stack.com](https://serverless-stack.com), where we use serverless-webpack. Whenever we make an update, we need to email our readers and let them know which packages and files need to be changed. This is obviously not ideal.

### How serverless-bundle works

To solve the above issues, serverless-bundle encapsulates all the necessary packages and configs with sensible defaults, so you only need to include one plugin.

```
-    "eslint"
-    "webpack"
-    "@babel/core"
-    "babel-eslint"
-    "babel-loader"
-    "eslint-loader"
-    "@babel/runtime"
-    "@babel/preset-env"
-    "serverless-webpack"
-    "source-map-support"
-    "webpack-node-externals"
-    "eslint-config-strongloop"
-    "@babel/plugin-transform-runtime"
-    "babel-plugin-source-map-support"

+    "serverless-bundle": "^1.2.2"
```

It works in much the same way as Create React App. Now when we need to apply a change to our Webpack config, we simply update the plugin and all our apps can be updated.

To get started, install the plugin:

``` bash
$ npm install --save-dev serverless-bundle
```

Then add it to your `serverless.yml`.

``` yaml
plugins:
  - serverless-bundle
```

And that's it! All your Lambda packges will now be optimized, your code will be linted, source maps will be generated with proper line numbers for debugging, and the build process will be cached to speed up your subsequent builds.

The serverless-bundle plugin also helps run your tests. It applies the same config it uses to transpile your code. All you need to do is add this to your `package.json`.

```
"scripts": {
  "test": "serverless-bundle test"
}
```

### Roadmap

We included the serverless-bundle plugin in our ever popular [Serverless Node.js Starter](https://github.com/AnomalyInnovations/serverless-nodejs-starter). If your project is based on an older version of our Node.js starter, we have [upgrade instructions here](https://github.com/AnomalyInnovations/serverless-nodejs-starter/releases/tag/v2.0). By open-sourcing we want to continue to build on it to help tackle a few of the other local development issues that Serverless folks tend to run into. We want to do this while minimizing the amount of configuration and complexity that developers need to manage.

If you'd like to help contribute or support the project, make sure to [star the serverless-bundle page on GitHub](https://github.com/AnomalyInnovations/serverless-bundle).
