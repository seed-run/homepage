---
layout: docs
title: Caching Dependencies
---

[Seed](/) automatically caches dependencies to speed up your builds. Currently dependency cache is available for Node.js projects. If you would like support for other runtimes, feel free to [contact us](mailto:{{ site.email }}). This speeds up your builds if you are using Node.js. But it also speeds up deployments for other runtimes that are using Serverless Framework plugins.

### Node.js

Here is how it works for Node.js projects.

- Seed auto-detects the package manager based on the `yarn.lock` or `package-lock.json` file. 
  - If Yarn is detected, Seed will cache the `node_modules` directory in the project root along with the Yarn cache.
  - If instead, npm is detected, Seed will cache `node_modules` directory in the project root.
- In the _Init_ step of the build process, Seed will restore the dependency cache. And in the _Cleanup_ step of the build process, Seed will update the dependency cache.
- Dependencies are cached on a per-stage basis. So when deploying a stage, the cache for that stage is loaded up.
- Finally to clear the cache, you can use the **Force deploy** option while [triggering a manual deployment]({% link _docs/manually-deploying.md %}#force-deploys).

A quick note on the impact of caching dependencies on build minutes. The time it takes to restore the cache counts towards the build minutes of your account. While the time to update the build cache does not.
