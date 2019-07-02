# How to manage secrets for your Serverless app?

Look at this concrete example:
```
import Stripe from 'stripe';
const stripe = Stripe('YOUR_STRIPE_SECRET_KEY');
```
Where does YOUR_STRIPE_SECRET_KEY come from?


- Local env.yml solution:
  1. create a env.yml
  ```
  stripeSecretKey: "sk_xxxx"
  ```
  1. reference env.yml in serverless.yml as Lambda environment variable
  ```
  provider:
    environment:
      stripeSecretKey: ${file(env.yml):stripeSecretKey}
  ```
  1. you can reference in your code as a normal environment variable
  ```
  const stripe = Stripe(process.env.stripeSecretKey);
  ```
  1. make sure the env.yml is not committed to git by adding it to .gitignore file

  PROS: does not rely on other AWS/3rd-party services
  
  CONS: env.yml lives in your locoal environment, cannot share within a team


- Store in your CI/CD provider
  Most CI/CD providers like Circle, Travis, and of course Seed, lets you store environment variables on their side and made available to you on deploy time, so you don't have to commit them in your code.
  1. add the secrets in your provider's console
  1. because the secrets are available as build-time environment variables, reference them in serverless.yml as Lambda environment variable
  ```
  provider:
    environment:
      stripeSecretKey: ${env:stripeSecretKey}
  ```
  1. you can reference in your code the same way
  ```
  const stripe = Stripe(process.env.stripeSecretKey);
  ```
  PROS: you can use this along with a local env.yml file for both local and remote usage while keeping your Lambda code the same, ie. process.env.stripeSecretKey
  
  CONS: you have to trust your CI/CD provider to keep your secrets safe


- Store in AWS Parameter Store
  AWS Systems Manager Parameter Store (SSM) is an AWS service that lets you store configuration data and secrets as key-value pairs in a central place. The values can be stored as plain text or encrypted data. When stored as encrypted data, the value is encrypted using your KMS key on store, and decrypted on read.
  1. add the secrets in your [AWS Parameter Store console](https://console.aws.amazon.com/systems-manager/parameters?region=us-east-1)
  1. reference the value in serverless.yml as Lambda environment variable. Serverless Framework is able to fetch the value from your AWS Parameter Store account on deploy.
  ```
  provider:
    environment:
      stripeSecretKey: ${ssm:stripeSecretKey}
  ```
  1. you can reference in your code the same way
  ```
  const stripe = Stripe(process.env.stripeSecretKey);
  ```
  PROS: you don't have to expose your secrets to 3rd party service. And again, you can use this along with a local env.yml file for both local and remote usage while keeping your Lambda code the same, ie. process.env.stripeSecretKey
  
  CONS: because the secretes are decrypted and then set as Lambda environment variable during deployment, if you go to your Lambda console, you can see the secret value in plain text
  
- Store in AWS Parameter Store, and decrypt at runtime
  1. change your Lambda code to call Parameter Store and decrypt the value at runtime
  ```
  const aws = require('aws-sdk');
  const ssm = new aws.SSM();
  const stripeSecretKey = ssm.getParameter({ Name:'stripeSecretKey', WithDecryption:true }).promise();
  const stripe = Stripe(stripeSecretKey.Parameter.Value);
  ```
  PROS: your secrets are not exposed in plain text at rest anywhere
  
  CONS: your Lambda code gets more complicated, and a latency is added to fetch the secret value
  
