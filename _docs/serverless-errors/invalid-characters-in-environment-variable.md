---
layout: build-errors
title: Invalid characters in environment variable
image: /assets/social-cards/common-errors.png
description: Invalid characters in environment variable
---

#### Error Message

> Invalid characters in environment variable


#### Problem

A common mistake that can lead to this error is defining environment variables as an array instead of key-value pairs. For example:

``` yml
...

provider:
  environment:
    - foo: abc
    - bar: xyz

...
```

#### Solution

Make sure the environment variables are defined in the YAML key-value pair format.

``` yml
...

provider:
  environment:
    foo: abc
    bar: xyz

...
```
