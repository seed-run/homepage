---
layout: post
title: Build Minutes Usage Info
categories: news
author: jack
---

We rolled out an update to the Seed console to clearly show the build minutes usage for each build.

![Build minutes usage in build logs](/assets/blog/build-minutes-usage-info/build-minutes-usage-in-build-logs.png)

Now you can see clearly how long each build took and the build minutes used as a part of that build.

```
> INFO: Build deployed in 1m 23s. Used 2 build minutes.
```

Recall that the build minutes are the amount of time a build process took, rounded up to the nearest minute. You'll notice that while the build process goes on to complete some additional steps (building artifacts for other stages, etc.), it doesn't contribute to the overall build minutes used.

You can also see additional details if you are using our high performance build containers.

![Build minutes usage for higher performance build containers](/assets/blog/build-minutes-usage-info/build-minutes-usage-for-higher-performance-build-containers.png)

Here you'll notice that the 2x performance container use double the build minutes as the standard containers.

```
> INFO: Build completed in 46s on Medium 2x container. Used 2 build minutes.
```

High performance build containers are available as a part of our custom pricing plans. [Contact us](mailto:{{ site.email }}) if you'd like to enable this for your organization.
