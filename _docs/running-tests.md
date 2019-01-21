---
layout: docs
title: Running Tests
---

Seed can automatically run the tests for your app. This is turned off initially, to allow you to set things up.

### Enable Unit Tests

To enable running unit tests for your app, head over to your app settings. And hit **Enable Unit Tests**.

![Enable unit tests](/assets/docs/running-tests/enable-unit-tests.png)

Once enabled, Seed will automatically detect and run your unit tests using the commands for the language/platform you are using.

### Node.js

For Node.js we run the tests you have defined in your project's `package.json` for the `test` script by running the following as a part of our build process.

``` bash
$ npm run test
```

For example, in your `package.json` you could have the following.

```
...
  "scripts": {
    "test": "jest"
  },
...
```

Here we are using [Jest](http://facebook.github.io/jest/) to run our tests.

If the test script is not found in the `package.json`, then the tests are skipped and the build is directly deployed.


### Python

For Python we use the following command to run the tests in your project.

``` bash
$ python -m unittest discover -s tests
```

This looks for the tests in the `tests/` directory.


Finally, Seed will deploy your stage if the tests pass successfully.
