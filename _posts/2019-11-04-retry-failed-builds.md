---
layout: post
title: Retry failed builds
categories: news
author: jack
---

You can now retry failed builds in Seed. The build status pages now gives you an option to retry a failed build.

![Failed build status page](/assets/blog/retry-failed-builds/failed-build-status-page.png)

Retrying a failed build uses the exact same commit to rerun the build process. This is especially useful for cases where you need to retry a build when there are no code changes to push. So for example, a build might have failed because an environment variable wasn't set. You can now update the environment and simply retry the failed build. 

We think this little change will be helpful when debugging any build issues that you might have.
