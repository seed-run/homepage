---
layout: docs
title: Adding Python Projects
---

Seed makes it really easy to deploy Serverless Python projects. We support:

- Python 2.7, 3.6, 3.7, and 3.8
- Unit tests using [unittest](https://docs.python.org/2/library/unittest.html#module-unittest)
- Support for the [serverless-python-requirements](https://github.com/UnitedIncome/serverless-python-requirements) plugin
- Dependencies using [pip](https://pypi.org/project/pip/) & [pipenv](https://pipenv.readthedocs.io)

Non-Python modules usually need to be built on your local machine using a Docker image that targets the Lambda environment.

Seed automatically builds non-Python modules for the target Lambda environment without having to compile them locally.

If you are using the [serverless-python-requirements](https://github.com/UnitedIncome/serverless-python-requirements) plugin you can disable building modules locally by turning off the `dockerizePip` setting.

``` yaml
custom:
  pythonRequirements:
    dockerizePip: false
```

We also have a [Serverless Python 3.6 Starter](https://github.com/AnomalyInnovations/serverless-python-starter) and a [Serverless Python 3.7 Starter](https://github.com/fwang/serverless-python3.7-starter) that you can use.
