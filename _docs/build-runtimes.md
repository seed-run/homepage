---
layout: docs
title: Build Runtimes
---


### General Purpose v2.0
Docker image: aws/codebuild/standard:3.0
      OS: Ubuntu 18.04
      nodejs: 12
      python: 3.8
      ruby: 2.6
      golang: 1.13
      dotnet: 3.0
      java: openjdk11
      php: 7.3
      npm: 6.13.4
      docker: 19.03 (if enabled)
      docker compose:=1.24 (if enabled)

### General Purpose v1.0
Docker image: aws/codebuild/standard:2.0
      OS: Ubuntu 18.04
      nodejs: 10
      python: 3.7
      golang: 1.13
      ruby: 2.6
      dotnet: 2.2
      java: openjdk11
      php: 7.3
      npm: 6.13.4
      docker: 18.09 (if enabled)
      docker compose:=1.24 (if enabled)

### Python 3.7 (DEPRECATED, upgrade to General Purpose v1.0)
Docker image: anomalyinnovations/python:3.7.0
      OS: Debian 9
      nodejs: 8.15
      python: 3.7
      npm:  6.1.0
      pip: 18.1

### Python 3.6
Docker image: anomalyinnovations/python:3.6.4-npm6.1.0-stretch
      OS: Debian 9
      nodejs: 8.15
      python: 3.6
      npm: 6.1.0
      pip: 9.0.1

### Python 2.7
Docker image: anomalyinnovations/python:2.7.14-npm6.1.0-stretch
      nodejs: 8.15
      python: 2.7
      npm: 6.1.0
      pip: 9.0.1

### Ruby 2.5
Docker image: anomalyinnovations/ruby:2.5.3
      OS: Debian 9
      nodejs: 8.10
      ruby: 2.5
      npm: 6.1.0

### .NET 2.1 (DEPRECATED, upgrade to General Purpose v1.0)
- Docker image: anomalyinnovations/dotnetcore:2.1.403
      OS: Debian 9
      nodejs: 8.10
      dotnet: 2.1
      npm: 6.1.0

