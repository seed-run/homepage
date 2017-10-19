---
layout: page
title: Running Tests
---

Seed automatically runs the tests you have defined in your project's `package.json`.

```
...
  "scripts": {
    "test": "jest"
  },
...
```

In the example above we are using [Jest](http://facebook.github.io/jest/) to run our tests.

Seed will deploy your stage if the tests pass successfully. If the test script is not found in the `package.json`, then the tests are skipped and the build is directly deployed.
