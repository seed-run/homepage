---
layout: docs
title: Adding Java Projects
---

Seed gives you a zero-config way to deploy Serverless Java projects. We currently support:

- Java 8
- Java 11

Seed also provides out-of-the-box support for the following ways to build your project:

1. Using [Maven](https://maven.apache.org/what-is-maven.html)
2. Using [Gradle](https://gradle.org)

### Using Maven

Seed first checks if you have a `pom.xml` file in your project. If so, then it assumes that you have the right steps for building your project.

We have a simple starter repo with the [Maven example here](https://github.com/seed-run/serverless-java-maven-starter).

### Using Gradle

If a `pom.xml` is not found, then Seed will look to see if you have a `build.gradle` file in your project. If you do, then it will run the following while building your project:

``` bash
$ gradle wrapper
$ ./gradlew build
```

We also have a simple starter repo with the [Gradle example here](https://github.com/seed-run/serverless-java-gradle-starter).

Once the project has been built (with either of the two above approaches), Seed continues the standard Serverless deployment process.
