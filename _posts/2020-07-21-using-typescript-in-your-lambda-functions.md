---
layout: post
title: Using TypeScript in your Lambda functions
image: assets/social-cards/serverless-bundle.png
description: To use TypeScript in your Lambda functions, simply include the serverless-bundle plugin. The serverless-bundle plugin is a zero-config way to generate optimized packages for your Node.js Lambda functions.
categories: community
image: assets/social-cards/serverless-typescript.png
author: jay
---

You can now use TypeScript in your Lambda functions by simply including the [serverless-bundle](https://github.com/AnomalyInnovations/serverless-bundle) plugin. 

![serverless-bundle plugin npm screenshot](/assets/blog/using-typescript-in-your-lambda-functions/serverless-bundle-plugin-npm-screenshot.png)

The serverless-bundle plugin optimally packages your Node.js Lambda functions with sensible defaults so you **don't have to maintain your own Webpack configs**. Thanks to a [community-wide effort](https://github.com/AnomalyInnovations/serverless-bundle/issues/61), serverless-bundle now supports TypeScript as well!

To use the new version of [serverless-bundle](https://github.com/AnomalyInnovations/serverless-bundle), install the NPM package.

``` bash
$ npm install --save-dev --save-exact serverless-bundle@2.0.0
```

Add it to your `serverless.yml`.

``` yaml
plugins:
  - serverless-bundle
```

And to run your tests, update your `package.json` with:

``` json
"scripts": {
  "test": "serverless-bundle test"
}
```

If you have a `tsconfig.json`, serverless-bundle will automatically compile your TypeScript files. If you need to specify it by name, add the following to your `serverless.yml`.


``` yml
custom:
  bundle:
    tsConfig: 'tsconfig.special.json'
```

For a full list of options, make sure to [check out our README](https://github.com/AnomalyInnovations/serverless-bundle/blob/master/README.md).

So give serverless-bundle a try in your projects, and [make sure to star it on GitHub](https://github.com/AnomalyInnovations/serverless-bundle)! ⭐
