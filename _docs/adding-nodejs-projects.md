---
layout: docs
title: Adding Node.js Projects
---

Seed provides first-class support for [Node.js](https://nodejs.org/) projects. We currently support:

- Node.js 18.x, 16.x, 14.x, 12.x, 10.x, 8.10, & 6.10
- Dependencies built using [npm](https://www.npmjs.com). We also support [private npm modules]({% link _docs/private-npm-modules.md %}).
- Unit tests via the `npm run test` command. You can read more on [running tests here]({% link _docs/running-tests.md %}).
- Most common Serverless plugins including, [Serverless Webpack](https://github.com/serverless-heaven/serverless-webpack).

Seed auto-detects the package manager. If a `yarn.lock` is found then Yarn will be used, And if `package-lock.json` is found then npm will be used. If neither are found then Seed defaults to npm.

#### Transition to npm 7

[npm 7 has a couple of breaking changes](https://github.blog/2021-02-02-npm-7-is-now-generally-available/), including a new lockfile format. This means that the new lockfile is incompatible with previous versions of npm. To help with this transition, if Seed detects the newer lockfile format, it'll automatically use npm 7 to install the dependencies.

We also have a popular starter project you can use - [Serverless Node.js Starter](https://github.com/AnomalyInnovations/serverless-nodejs-starter).
