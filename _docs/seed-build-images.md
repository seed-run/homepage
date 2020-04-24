---
layout: docs
title: Seed Build Images
---

Seed runs your builds inside a virtual machine and it'll use a build image based on the Lambda runtime of your service. Below is a list of all the images in use:

[**Active Images**](#build-images)
- [General Purpose v3.0](#general-purpose-v30)
- [General Purpose v1.0](#general-purpose-v10)
- [Python 3.6](#python-36)
- [Python 2.7](#python-27)
- [Ruby 2.5](#ruby-25)

[**Deprecated Images**](#deprecated-build-images)
- [General Purpose v2.0](#general-purpose-v20)
- [Python 3.7](#python-37)
- [.NET Core 2.1](#net-core-21)


To check which build image is being used, head over to the build logs for your build.

![Build image info in build logs](/assets/docs/seed-build-images/build-image-info-in-build-logs.png)

## Build Images

Below are the build images that are used and the types of services they are used for. A build image is chosen based on the Lambda runtime of the service.

### General Purpose v3.0

Lambda runtimes: Node.js 12.x, Python 3.8, Go 1.x, Ruby 2.7, Java 11

OS: Ubuntu 18.04

| Includes        | Version |
|-----------------|:-------:|
| Node.js         | 12.16.1 |
| Python          | 3.8.1   |
| Ruby            | 2.7.0   |
| Go              | 1.14    |
| .NET Core       | 3.1.102 |
| Java            | 11.0.5  |
| PHP             | 7.4.1   |
| NPM             | 6.13.4  |
| YARN            | 1.22.0  |
| PIP             | 19.3.1  |
| Docker*         | 19.03.3 |
| Docker Compose* | 1.24.0  |

*[Docker and Docker Compose need to be enabled.]({% link _docs/docker-commands-in-your-builds.md %})

### General Purpose v1.0

Lambda runtimes: Node.js 10.x, Python 3.7, Java 8, .NET Core 2.1

OS: Ubuntu 18.04

| Includes        | Version |
|-----------------|:-------:|
| Node.js         | 10      |
| Python          | 3.7     |
| Ruby            | 2.6     |
| Go              | 1.13    |
| .NET Core       | 2.2     |
| Java            | 11      |
| PHP             | 7.3     |
| NPM             | 6.13.4  |
| YARN            | 1.12.3  |
| PIP             | 19.3.1  |
| Docker*         | 18.09   |
| Docker Compose* | 1.24    |

*[Docker and Docker Compose need to be enabled.]({% link _docs/docker-commands-in-your-builds.md %})

### Python 3.6

Lambda runtime: Python 3.6

OS: Debian 9

| Includes        | Version |
|-----------------|:-------:|
| Node.js         | 8.15    |
| Python          | 3.6     |
| NPM             | 6.1.0   |
| YARN            | 1.12.3  |
| PIP             | 9.0.1   |

### Python 2.7

Lambda runtime: Python 2.7

OS: Debian 9

| Includes        | Version |
|-----------------|:-------:|
| Node.js         | 8.15    |
| Python          | 2.7     |
| NPM             | 6.1.0   |
| YARN            | 1.12.3  |
| PIP             | 9.0.1   |

### Ruby 2.5

Lambda runtime: Ruby 2.5

OS: Debian 9

| Includes        | Version |
|-----------------|:-------:|
| Node.js         | 8.10    |
| Ruby            | 2.5     |
| NPM             | 6.1.0   |
| YARN            | 1.12.3  |

---

## Deprecated Build Images

The following build images are no longer available for new services but might still be in use for existing services. If your services are still using the ones below, [contact us](mailto:{{ site.email }}) to have them upgraded.

### General Purpose v2.0

Upgrade to: [General Purpose v3.0](#general-purpose-v30)

OS: Ubuntu 18.04

| Includes        | Version |
|-----------------|:-------:|
| Node.js         | 12      |
| Python          | 3.8     |
| Ruby            | 2.6     |
| Go              | 1.13    |
| .NET Core       | 3.0     |
| Java            | 11      |
| PHP             | 7.3     |
| NPM             | 6.13.4  |
| YARN            | 1.12.3  |
| PIP             | 19.3.1  |
| Docker*         | 19.03   |
| Docker Compose* | 1.24    |

*[Docker and Docker Compose need to be enabled.]({% link _docs/docker-commands-in-your-builds.md %})

### Python 3.7

Upgrade to: [General Purpose v1.0](#general-purpose-v10)

Lambda runtime: Python 3.7

OS: Debian 9

| Includes        | Version |
|-----------------|:-------:|
| Node.js         | 8.15    |
| Python          | 3.7     |
| NPM             | 6.1.0   |
| YARN            | 1.12.3  |
| PIP             | 18.1    |

### .NET Core 2.1

Upgrade to: [General Purpose v1.0](#general-purpose-v10)

Lambda runtime: .NET Core 2.1

OS: Debian 9

| Includes  | Version |
|-----------|:-------:|
| Node.js   | 8.10    |
| .NET Core | 2.1     |
| NPM       | 6.1.0   |
| YARN      | 1.12.3  |

## Changing the Build Image

Once your service has been successfully deployed, Seed does not change the build image. If you want to use a different build image for a service, you'll need to [contact us](mailto:{{ site.email }}). In the future we'll be making this option configurable.
