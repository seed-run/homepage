---
layout: docs
title: Adding Node.js Projects
---

Seed provides first-class support for [Node.js](https://nodejs.org/) projects. We currently support:

- Node.js 14.x, 12.x, 10.x, 8.10, & 6.10
- Dependencies built using [npm](https://www.npmjs.com). We also support [private npm modules]({% link _docs/private-npm-modules.md %}).
- Unit tests via the `npm run test` command. You can read more on [running tests here]({% link _docs/running-tests.md %}).
- Most common Serverless plugins including, [Serverless Webpack](https://github.com/serverless-heaven/serverless-webpack).

Seed auto-detects the package manager. If a `yarn.lock` is found then Yarn will be used, And if `package-lock.json` is found then npm will be used. If neither are found then Seed defaults to npm.

We also have a popular starter project you can use - [Serverless Node.js Starter](https://github.com/AnomalyInnovations/serverless-nodejs-starter).
