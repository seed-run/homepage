---
layout: docs
title: Adding Java Projects
---

Seed gives you a zero-config way to deploy Serverless Java projects. We provide out-of-the-box support for the following ways to build your project:

1. Using Maven
2. Using Gradle

### Using Maven

Seed first checks if you have a pom.xml file in your project. If so, then it assumes that you have the right steps for building your project.

We have a simple starter repo with the [Maven example here](https://github.com/fwang/serverless-java-maven-starter).

### Using Gradle

If a pom.xml is not found, then Seed will look to see if you have a build.gradle file in your project. If you do, then it will run the following while building your project:

- `$ gradle wrapper`
- `$ ./gradlew build`

We also have a simple starter repo with the [Gradle example here](https://github.com/fwang/serverless-java-gradle-starter).

Once the project has been built (with either of the two approaches), Seed continues the standard Serverless deployment process.
