---
layout: post
title: serverless-bundle v5
image: assets/social-cards/serverless-bundle-v5.png
categories: community
author: jay
---

The ever popular [serverless-bundle](https://github.com/AnomalyInnovations/serverless-bundle) plugin has a new major update. The v5 release features a slew of improvements, support for esbuild, Webpack 5, etc.

[![serverless-bundle plugin npm screenshot](/assets/blog/serverless-bundle-v5/serverless-bundle-plugin-npm-screenshot.png)](https://github.com/AnomalyInnovations/serverless-bundle)

We [open sourced the serverless-bundle plugin]({% link _posts/2019-07-22-introducing-the-serverless-bundle-plugin.md %}) a little over two years ago. It provides a zero-config way to bundle your Lambda functions with Webpack, without having to maintain dozens of packages or configs. Since it's launch, it's grown to become one of the most popular Serverless Framework plugins.

Earlier this week, thanks to some amazing community contributions, we [released v5 of the plugin](https://github.com/AnomalyInnovations/serverless-bundle/releases/tag/v5.0.0).

It features:

- Support for [esbuild](https://esbuild.github.io/) via the [esbuild-loader](https://github.com/privatenumber/esbuild-loader) Webpack plugin. This can really speed up your builds.

- Using esbuild to minimize functions. Further reducing the size of a Lambda function.

- Update to Webpack 5.

- Support for [serverless-webpack](https://www.github.com/serverless-heaven/serverless-webpack)'s concurrency setting.

- And much more. [Head over to the release notes for more details](https://github.com/AnomalyInnovations/serverless-bundle/releases/tag/v5.0.0).

A huge thanks to [Thomas Schaaf](https://github.com/thomaschaaf) for helping put this together!


