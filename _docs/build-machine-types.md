---
layout: docs
title: Build Machine Types
---

Seed runs your builds inside a virtual machine and there are three different machine types that can be used.

| Build Machine | Memory | vCPU | Build Minutes Used |
|---------------|:------:|:----:|:------------------:|
| Standard      | 3GB    | 2    | 1x                 |
| Medium        | 7GB    | 4    | 2x                 |
| Large         | 15GB   | 8    | 4x                 |

Note that, by default your builds are run in a **Standard 1x** build machine.

The Standard build machine should work for most build processes. However, there might be cases where your builds might run out of memory or you might be looking to speed up your builds.

To use a high performance build machine, head over to your app pipeline a select the service that you want to configure.

![Build machine options in service settings](/assets/docs/build-machine-options/build-machine-options-in-service-settings.png)

Here you'll be able to select a different build machine. And moving forward all the builds on the service will use this new build machine.

The **Build Minutes Used** above are the amount of build minutes that will be used in a build process. So for example.

If a build process takes 2 minutes to complete:
  - It'll take 1 x 2 minutes = 2 build minutes in a Standard build machine,
  - 2 x 2 minutes = 4 build minutes in a Medium,
  - And 4 x 2 minutes = 8 build minutes in a Large build machine.

To look at the amount of build minutes used, head over to the build logs.

![Build minutes usage in build logs](/assets/docs/build-machine-options/build-minutes-usage-in-build-logs.png)

You'll notice how long the build process took, and given the build machine used, the amount of build minutes it used.
