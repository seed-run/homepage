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

To use a high performance build machine, head over to your **app settings** > select the **service** that you want to configure > and edit the **Build Machine** option.

![Build machine options in service settings](/assets/docs/build-machine-types/build-machine-options-in-service-settings.png)

Here you'll be able to select a different build machine. And moving forward all the builds on the service will use this new build machine.

The **Build Minutes Used** above are the amount of build minutes that will be used in a build process. So for example.

If a build process takes 2 minutes to complete:
  - It'll take 1 x 2 minutes = 2 build minutes in a Standard build machine,
  - 2 x 2 minutes = 4 build minutes in a Medium,
  - And 4 x 2 minutes = 8 build minutes in a Large build machine.

To look at the amount of build minutes used, head over to the build logs.

![Build minutes usage in build logs](/assets/docs/build-machine-types/build-minutes-usage-in-build-logs.png)

You'll notice how long the build process took, and given the build machine used, the amount of build minutes it used.

### Second Generation Machines

Second Generation build machines are currently in beta and are designed to startup 6 times faster than the current set of build machines. Resulting in much faster build times.

The specs for the Second Generation machines are identical to the current generation.

| Build Machine | Memory | vCPU | Build Minutes Used |
|---------------|:------:|:----:|:------------------:|
| Standard SG   | 3GB    | 2    | 1x                 |
| Medium SG     | 7GB    | 4    | 2x                 |
| Large SG      | 15GB   | 8    | 4x                 |

Note the postfix **_SG_** that's used to denote the difference between the two types.

During the beta you can select one of the Second Generation machines from a service's settings. Just as mentioned above.

And you can find which machine was used for a given build at the top of your build logs.

![Build machine info in build log](/assets/docs/build-machine-types/build-machine-info-in-build-log.png)

During the beta we'll be scaling up capacity for the Second Generation machines. So you might occasionally find Seed falling back to using the First Generation version of the build machine you selected.

![Build machine fallback info in build log](/assets/docs/build-machine-types/build-machine-fallback-info-in-build-log.png)

Above you'll notice that Seed is falling back to the First Generation machine.
