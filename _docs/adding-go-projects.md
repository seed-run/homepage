---
layout: docs
title: Adding Go Projects
---

Seed gives you a zero-config way to deploy Serverless Go projects. We provide out-of-the-box support for the following ways to build your project:

1. Using the Makefile
2. Using the [serverless-go-build](https://github.com/sean9keenan/serverless-go-build) plugin

### Using the Makefile

Seed first checks if you have a Makefile in your project. If so, then it assumes that you have the right steps for building your project.

We have a simple starter repo with the [Makefile example here](https://github.com/fwang/serverless-go-starter).

### Using the serverless-go-build Plugin

If a Makefile is not found then Seed will look to see if you are using the [serverless-go-build plugin](https://github.com/sean9keenan/serverless-go-build). If you are, then it will run the following while building your project:

- Install the dependencies using `dep ensure`. Where [dep](https://github.com/golang/dep) is the dependency manager for Go.
- Run `serverless build`.

We also have a simple starter repo with the [serverless-go-build example here](https://github.com/fwang/serverless-go-starter-with-plugin).

Once the project has been built (with either of the two approaches), Seed continues the standard Serverless deployment process.