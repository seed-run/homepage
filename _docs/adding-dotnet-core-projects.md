---
layout: docs
title: Adding .NET Core Projects
---

Seed gives you a simple way to manage deployments for your .NET Core 2.1 & 3.1 projects. We provide out-of-the-box support for the following ways to build your projects:

1. Using a `build.sh` script
2. Using the [serverless-dotnet](https://github.com/fruffin/serverless-dotnet) plugin

### Using a build script

Seed will check if you have a `build.sh` at the root of your project (or service). If it finds one then it will run the script before doing a serverless build.

We have a couple of starter projects to illustrate how this works:

- [C#](https://github.com/seed-run/serverless-csharp-starter)
- [F#](https://github.com/seed-run/serverless-fsharp-starter)

### Using the serverless-dotnet plugin

In addition to the `build.sh` script, Seed will look to see if you are using the [serverless-dotnet](https://github.com/fruffin/serverless-dotnet) plugin. If you are, then it will run the script before a serverless build.

We have a [simple starter project with the serverless-dotnet plugin as well](https://github.com/seed-run/serverless-csharp-starter-with-plugin).
