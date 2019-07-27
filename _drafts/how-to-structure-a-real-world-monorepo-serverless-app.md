# How to structure a real world Monorepo Serverless app?

We are going to answer these questions:
- how to structure package.json
- how to share common code among services
- how to share common config in code among services
- how to share common config for serverless.yml
- how to reference resources in another service, and deploy phase

Let's use a real world example. Assume you are running an online store, and when a customer makes a purchase, you need to process the payment. Once the payment goes through you will send out a confirmatioin email and start the shipping process at the same time. To facilitate this, we are going to build a Serverless app with:
- An API service that processes the payment. And if the payment goes through, it will publish a PURCHASED message;
- A service that listens for the PURCHASED message and sends out the confirmation email;
- A service that also listens for the PURCHASED message and creates a shipping record in the database.

The code structure looks like below. You can find the source code here - https://github.com/seed-run/serverless-example-monorepo-with-code-sharing
```
/
  package.json
  config.yml
  libs/
  services/
    purchase-api/
      package.json
      serverless.yml
      handler.js
    confirmation-job/
      serverless.yml
      handler.js
    shipping-job/
      serverless.yml
      handler.js
```

# How to structure package.json?
- Dependencies shared across the services go into root level package.json. For example, all services use the 'serverless-bundle' plugin for packaging the Lambda functions.
- Dependencies used specifically in a service go into the service level package.json. For example, the purchase-api service uses the 'stripe' module to call Stripe APIs.
- When deploying the app in the CI environment, need to run 'npm install' in both the root level and inside each services.

Normally, you have to manually pick and choose which modules need to be packaged with your Lambda function. Simply packaging all dependencies with your Lambda function will increase the code size of your Lambda function and leads to performance impact such as longer cold start time. In our example, we are going to use the 'serverless-bundle' plugin to help us to just do that by using webpack and apply tree shaking while packaging the Lambda code.

# How to share common code among services
- Place common code in the libs folder. For example, the services need to make various calls to other AWS services through AWS SDK. And we are going to put the SDK configuration code in the libs folder.

# How to share common config for serverless.yml
- Place shared config values in a common yaml file at the root level
- Imagine, we need to set the timeout for our Lambda functions to 20 seconds for all services. Create a config.yml at the root
```
timeout: 20
```
- And in each service's serverless.yml
```
...
provider:
  name: aws
  timeout: ${file(../../config.yml):timeout}
...
```

# How to reference resources in another service, and deploy phase
In purchase-api, we created a SNS topic. For the job services to be able to subscribe to the topic, purchase-api needs to export the ARN of the topic. To export, in purchase-api's serverless.yml:
```
...

resources:
  Resources:
    PurchasedTopic:
      Type: AWS::SNS::Topic
      Properties:
        TopicName: ${opt:stage}-purchased

  Outputs:
    PurchasedTopicArn:
      Value:
        Ref: PurchasedTopic
      Export:
        Name: ${opt:stage}-PurchasedTopicArn
```
And in the job's serverless.yml
```
...
functions:
  handler:
    handler: handler.main
    events:
      - sns:
        'Fn::ImportValue': '${opt:stage}-PurchasedTopicArn'
```

This configuration makes the 2 jobs service dependent on the purchase-api service. When you deploy your app, purchase-api service needs to be deployed first, then the job services. Seed handles the service dependencies via deploy phase. You can defined the order in which you want the services to be deployed in.

# Benefit
- Common code always sit above the services level
- A code/config change above the services level affect all services
- A code/config change at the service level ONLY affects the specific service
- In a monorepo first CI/CD environment like Seed, following this structure helps the CI/CD service know on code change if a service is changed and needs to be deployed. For example, purchase-api does not need to be deployed if a commit only contains changes in the 'shipping-job' service folder.
