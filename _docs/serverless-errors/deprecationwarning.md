---
layout: common-errors
title: DeprecationWarning
image: /assets/social-cards/common-errors.png
description: "(node:8) [DEP0005] DeprecationWarning: Buffer() is deprecated due to security and usability issues. Please use the Buffer.alloc(), Buffer.allocUnsafe(), or Buffer.from() methods instead."
---

#### Error Message

You might see one of the following error messages, or something similar in your CloudWatch logs:

> (node:8) [DEP0005] DeprecationWarning: Buffer() is deprecated due to security and usability issues. Please use the Buffer.alloc(), Buffer.allocUnsafe(), or Buffer.from() methods instead.

> (node:8) DeprecationWarning: current URL string parser is deprecated, and will be removed in a future version. To use the new parser, pass option { useNewUrlParser: true } to MongoClient.connect.

#### Problem

`DeprecationWarning` errors are logged by the Node.js runtime when your code (or one of the dependencies in your code) calls a deprecated API. These warnings usually include a `DEP` deprecation code. They are logged using `console.error` and end up in your CloudWatch logs.

You can view [a full list over on the Node.js docs](https://nodejs.org/api/deprecations.html).

#### Solution

Even though these are logged as errors, they are really just warnings. This warning might be either printed out by a dependency, or by the Node.js runtime.

In either case, make sure you are not calling a deprecated Node.js API, and make sure to keep your dependencies up to date.

If you are using [Issues]({% link _docs/issues-and-alerts.md %}), Seed will [automatically ignore these warnings]({% link _docs/issues-and-alerts.md %}#automatically-ignored-issues).
