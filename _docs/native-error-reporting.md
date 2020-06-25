---
layout: docs
title: Native Error Reporting
---

[Issues]({% link _docs/issues-and-alerts.md %}) can detect most Lambda failures automatically. But errors and exceptions (the ones you catch in your code) need to be manually reported. To do this, simply log the error to the console and it'll get reported. We call this _Native Error Reporting_.

#### Advantages

And it has a few key advantages:

1. You **don't need to install** any 3rd party SDKs or libraries.
2. You **don't need any special code** to handle this. No wrappers or API calls. Simply `console.error`.
3. There is **no impact on performance**. If you are reporting to a 3rd party service, your Lambda function needs to wait till the call completes.
4. It works in your local environment. You can see these messages in your console.

#### Support

Currently Native Error Reporting is supported for:

- [Node.js](#nodejs) (10.x and above)
- [Python](#python) (3.7 and 3.8)

If you are interested in using it with another runtime, [let us know](mailto:{{ site.email }}) and we'll look into adding support for it.

In this chapter we'll look at some of the language specific details of Native Error Reporting. 

-----

### Node.js

Issues supports Node.js 10.x and above. Let's start by looking at some examples of how to report errors in Node.js 

- Handled exceptions
  
  Your code might have an exception, and you might not want your Lambda function to fail. But you want to report the error. For example, when handling API requests, you might want to catch the exception and return a JSON response.

  ``` javascript
  try {
    // Your code
  } catch(error) {
    // Report this error to Issues
    console.error(error);
    // Log some debug information to go along with it
    console.log('All the logs in this request will appear in the Issues page');
  }
  ```
  
  In the case of exceptions, Seed will group the ones that have similar stack traces together.

- Custom errors

  Similarly, you might want to report errors that happen outside of a try/catch block.

  ``` javascript
  // Report this error to Issues
  console.error('User object is undefined');
  // Log some debug information to go along with it
  console.log({ userObject });
  console.log('All the logs in this request will appear in the Issues page');
  ```
  
  In the case of custom errors, Seed uses the error message to group similar issues together.

-----

### Python

Issues supports Python 3.7 and 3.8. Let's look at how to report errors in Python.

- Handled exceptions

  If you catch an exception and would like to report the error without having your Lambda function fail:
  
  ``` python
  import logging

  logger = logging.getLogger()

  try:
    # Your code
  except Exception as e:
    # Report this error to Issues
    logger.exception(e)
    # Log some debug information to go along with it
    logger.info('All the logs in this request will appear in the Issues page')
  ```
  
  In the case of exceptions, Seed will group the ones that have similar stack traces together.

- Custom errors

  On the other hand, you might want to report errors that happen outside of a try/catch block.

  ``` python
  # Report this error to Issues
  logger.error('User object is undefined')

  # Log some debug information to go along with it
  logger.info('All the logs in this request will appear in the Issues page');
  ```

  In the case of custom errors, Seed uses the error message to group similar issues together.

#### Reporting with a custom log format

Seed relies on the default log format to detect errors. If you are using a custom log format, it won't be reported. To fix this there are a couple of options:

1. Add the new handler without overwriting the default handler

   ``` python
   # Wrong: don't overwrite default handler
   defaultHandler = logger.handlers[0]
   # Your custom log format
   defaultHandler.setFormatter(logging.Formatter("%(asctime)s %(levelname)s:%(message)s", "%Y-%m-%d %H:%M:%S"))
   
   # Correct: create a new handler
   newHandler = logging.StreamHandler()                                                             
   # Your custom log format
   newHandler.setFormatter(logging.Formatter("%(asctime)s %(levelname)s:%(message)s", "%Y-%m-%d %H:%M:%S"))
   logger.addHandler(newHandler)
   ```

   And then to report the error:

   ``` python
   # Report an exception to Issues
   try:
     # Your code
   except Exception as e:
     logger.exception(e)
   ```

2. Use a child logger at the root and create a new logger instance for reporting

   ```python
   # Wrong: don't use the root logger
   myLogger = logging.getLogger()
   
   # Correct: create a child logger
   myLogger = logging.getLogger('my-logger')
   ```

   And then while reporting an error, create a new logger.

   ``` python
   # Create a new logger to report issues to Seed
   errorLogger = logging.getLogger('error-logger')
   
   # Report an exception to Issues
   try:
     # Your code
   except Exception as e:
     errorLogger.exception(e)
   ```

#### Logger instead of print

If you are currently using the `print` command in your code to debug errors; switch the relevant lines to `logger.error` instead.

For example, you might have something like this:

``` python
print('Could not charge credit card')
print('Some more debug info to go with this')
```

Instead, change it to:

``` python
logger.error('Could not charge credit card')
print('Some more debug info to go with this')
```

This will get reported to Issues as the `Could not charge credit card` error. And the issue details will include the debug info in the `print` statement.

--------

### Patterns to Avoid

While reporting errors to Issues, there are a couple of simple patterns to avoid. These apply to all runtimes but we are going to look at some Node.js examples.

1. Avoid identifiers or timestamps in error messages

   The idea of grouping based on the error messages means that you should avoid using unique identifiers in your error messages. For example, if you report an error using:
   
   ``` javascript
   console.error(`Detected a Big Error at ${Date.now()}`);
   ```
   
   Every occurrence of this error will be displayed separately, instead of grouping them together! If you want to log this identifier, use a separate `console.log` like so:
   
   ``` javascript
   console.error('Big Error');
   console.log(`Detected at ${Date.now()}`);
   ```

2. Avoid calling `console.error` multiple times for the same error

   Each `console.error` call results in an error being reported. If there are multiple calls for the same error, they get reported as multiple issues.
   
   For example, avoid doing the following:
   
   ``` javascript
   try {
     // Your code
   } catch(e) {
     // Report the error
     console.error('Error loading user object');
     // Reports another error!
     console.error(e);
   }
   ```
   
   Instead, use a `console.debug` or `console.log` for the first `console.error` line.
