# Why Serverless deployment artifacts cannot be reused across stages?

In a normal CI/CD pipeline setup, a continuous integration workflow always starts with the build server pull the code and run basic unit tests against them. If the test pass, the code is packaged into an artifact and assigned a build id. The artifact then gets deployed to your dev environment for further tests. If the process goes smoothly, the same artifact propagates through various downstream stages and finally gets deployed to the production environment. This artifact is called an **Immutable Artifact**. The idea being, once the code is tested and packaged, the artifact is frozen. No changes are made to it as it propagates downstream. You might be a small team and only have a dev and a prod environment, but the idea holds true.

Unfortunately, this is not the case for Serverless apps. When you generate an artifact running `serverless package -s dev`, the artifact can only be used for the `dev` stage. Here is why. The artifact contains 3 parts, [A quick recap of how Serverless generates artifacts - link to the blog post]:

- one or more zip files containing the Lambda code for your service;
- a CloudFormation template file that describes the resources defined in your serverless.yml;
- a serverless-state.json file that is used internally by Serverless Framework.

The Lambda code is environment/stage agnostic, and can be re-used across environments. The CloudFormation template is stage specific because the stage name is used in resource naming. Consider this serverless.yml definition:
```
service: my-service
...
functions:
  billing:
    handler: path_to_handler_file/billing.main
    events:
      - http:
          path: /billing
```
If you run `serverless package -s dev` and inspect the generated CloudFormation template, you will see:

- an AWS::Logs::LogGroup resource named /aws/lambda/my-service-**dev**-billing
- an AWS::IAM::Role resource named my-service-**dev**-us-east-1-lambdaRole
- an AWS::Lambda::Function resource named my-service-**dev**-billing
- an AWS::ApiGateway::RestApi resource named **dev**-my-service

As you can see all resources names contains the name of the stage.

Note that you can re-use the same artifact when you want to rollback to a previous deployment within the same stage. But you do need to package once for each stage as your code propagates through your deployment pipeline.
