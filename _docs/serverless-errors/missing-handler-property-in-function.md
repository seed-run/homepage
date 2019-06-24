---
layout: build-errors
title: Missing "handler" property in function
image: /assets/social-cards/common-errors.png
description: 'Missing "handler" property in function "events". Please make sure you point to the correct lambda handler. For example: handler.hello. Please check the docs for more info'
---

#### Error Message

> Missing "handler" property in function "events". Please make sure you point to the correct lambda handler. For example: handler.hello. Please check the docs for more info


#### Problem

Each Lambda function needs to have a `handler` property pointing to the location of the handler function. In this case, Serverless Framework is not able to parse the handler property.


#### Solution

Ensure that the `handler` attribute is defined in the `serverless.yml` for the given function. If it is, then double-check the formatting of your `serverless.yml`.

Below are a couple of examples of poorly indented `serverless.yml` sections.

**Example 1**: The following would result in a `Missing "handler" property in function "hello".` error. Note how the `handler:` property is indented.

``` yml
...

functions:
  hello:
  handler: hello.main

...
```

**Example 2**: The following would result in a `Missing "handler" property in function "events".` error. Note how the `events:` block is indented.

```yml
...

functions:
  hello:
    handler: hello.main
  events:
      - http:

...
```

**Example 3**: The resources block is poorly indented as a function. And the resulting error would be: `Missing "handler" property in function "resources".`.

```yml
...

functions:
  hello:
    handler: hello.main

  resources:
  Outputs:
    UsersTableArn:

...
```

Note that a correctly formatted handler block has all its properties indented to the right of the function name.

```yml
...

functions:
  hello:
    handler: hello.main
    events:
        - http:

...
```
