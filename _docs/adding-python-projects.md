---
layout: docs
title: Adding Python Projects
---

Seed makes it really easy to deploy Serverless Python projects. We support:

- Python 2.7, 3.6, 3.7, and 3.8
- Unit tests using [unittest](https://docs.python.org/2/library/unittest.html#module-unittest)
- Support for the [serverless-python-requirements](https://github.com/UnitedIncome/serverless-python-requirements) plugin
- Dependencies using [pip](https://pypi.org/project/pip/) & [pipenv](https://pipenv.readthedocs.io)

Seed auto-detects the package manager. If a `Pipfile` is found then pipenv will be used, And if `requirements.txt` is found then pip will be used.

Non-Python modules usually need to be built on your local machine using a Docker image that targets the Lambda environment.

Seed automatically builds non-Python modules for the target Lambda environment without having to compile them locally.

If you are using the [serverless-python-requirements](https://github.com/UnitedIncome/serverless-python-requirements) plugin you can disable building modules locally by turning off the `dockerizePip` setting.

``` yaml
custom:
  pythonRequirements:
    dockerizePip: false
```

We also have a [Serverless Python 3.6 Starter](https://github.com/AnomalyInnovations/serverless-python-starter), a [Serverless Python 3.7 Starter](https://github.com/seed-run/serverless-python3.7-starter), and a [Serverless Pipenv Starter](https://github.com/seed-run/serverless-pipenv-starter) that you can use.
