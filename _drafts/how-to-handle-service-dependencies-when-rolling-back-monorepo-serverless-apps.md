# How to handle service dependencies when rolling back monorepo Serverless apps?

In a single-service Serverless app, the rollback strategy simply involves re-deploy the previously packaged deployment artifact.

However, in a monorepo setup, an app is made up of many Serverless services. And among the services, you have inter-service dependencies. These dependencies require the services to be deployed in specific orders. (link to the post 'Can I deploy the services in a monorepo Serverless app concurrently when there are inter dependencies between them?') Specific orders also need to be followed when rolling back such deployments with inter-service dependencies.

Let's consider the following monorepo setup as an example. The app has two Serverless Framework services, located inside the services/ folder.

    /
      package.json
      libs/
      services/
        serviceA/
          serverless.yml
          handler.js
        serviceB/
          serverless.yml
          handler.js

Now Let's take a look at 3 rollback scenarios.

### Scenario 1: rollback an update that added an inter-service dependency

Say you added an SNS topic named ATopic in ServiceA and exported the topic's ARN. Here is an example of ServiceA's serverless.yml:

    service: serviceA
    ...
    resources:
    	- Outputs:
    				ATopicArn:
    					Value:
    		        Ref: ATopic
    			    Export:
    		        Name: ATopicArn

And ServiceB imports the topic and uses it to trigger the 'topicHandler' function:

    service: serviceB
    ...
    functions:
      topicHandler:
        handler: handler.main
        events:
          - sns:
            'Fn::ImportValue': ATopicArn

You commit the changes and deploy the services. Note that serviceA had to be deployed first, such that the export value `ATopicArn` exists, and then deploys serviceB. Unfortunately after the services were deployed, your Lambda functions start to error out and you have to rollback. In this case, you need to:

> Rollback the services in the reverse order of the deployment

Meaning serviceB needs to be rolled back first, such that the exported value 'ATopicArn' is not used by other services, and then rollback serviceA to remove the SNS topic along with the export.

### Scenario 2: rollback an update that removed an inter-service dependency

Let's use a similar example. Say serviceA exported ATopicArn that was imported by serviceB. And you decide to remove the topic. This time around serviceB has to be deployed first, such that the exported value 'ATopicArn' is not used, and then deploys serviceA. Unfortunately after the services were deployed, you have to rollback. Again, you need to:

> Rollback the services in the reverse order of the deployment

Meaning serviceA needs to be rolled back first, such that the export value `ATopicArn` exists, and then rollback serviceB.

### Scenario 3: rollback an update that did not update inter-service dependency

This is the case when you made only code changes to your services, which is likely to be most of your commits. The deployment strategy is straight forward, you can deploy all of your services concurrently. And when you need to rollback, you simply:

> Rollback the services in any order

### Conclusion

Whenever you need to rollback your monorepo application, always rollback the services in the reverse order of how they deployed. This also apply to our third scenario, since the reverse order by deploying all services concurrently means rolling back concurrently.
