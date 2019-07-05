---
layout: post
title: Python Support
categories: news
author: jay
---

You can now deploy Python projects via Seed! Python 2.7 and 3.6 are supported. And dependencies are built using [Virtualenv](https://pypi.python.org/pypi/virtualenv).

Seed also supports the [serverless-python-requirements](https://github.com/UnitedIncome/serverless-python-requirements) plugin. And as an added bonus, you don't need to build using a Docker image since the Seed build environment mirrors the Lambda Python runtime. This greatly simplifies the CI/CD pipeline for Python Serverless projects.

Finally, unit tests using [unittest](https://docs.python.org/2/library/unittest.html#module-unittest) are run automatically as a part of the build process.

You can [read more about python support in our docs]({% link _docs/adding-python-projects.md %}).
