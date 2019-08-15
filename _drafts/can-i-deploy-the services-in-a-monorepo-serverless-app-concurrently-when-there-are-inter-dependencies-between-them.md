# Can I deploy the services in a monorepo Serverless app concurrently when there are inter dependencies between them? 

The short answer is:
- No when you introduce a new dependency in the deployment; and
- Yes when you deploy with existing dependencies.

Here is why. Let's consider the following monorepo architecture as an example. The app has three Serverless Framework services, located inside the services/ folder.
```
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
        serviceC/
          serverless.yml
          handler.js
```
Say ServiceA creates an SNS topic and exports the topic's ARN in its serverless.yml:
```
    service: serviceA
    ...
    resources:
      - Outputs:
          ATopicArn:
    	    Value:
    		  Ref: ATopic
    		Export:
    		  Name: ATopicArn
```
And ServiceB and ServiceC uses the SNS topic as their Lambda triggersss:
```
    service: serviceB
    ...
    functions:
      handler:
        handler: handler.main
        events:
          - sns:
            'Fn::ImportValue': ATopicArn
```
### No, you cannot deploy concurrently

If you are deploying for the first time, you have to deploy serviceA first, such that the export value `ATopicArn` exists, and then deploy serviceB and serviceC. If you were to deploy all three services concurrently, serviceB and serviceC will fail as CloudFormation will complain:

`serviceB - No export named ATopicArn found.`

### Yes, you can deploy concurrently

Once you have deployed the three services successfully once, you can deploy them concurrently on subsequent deployments.

### No, you cannot again

Say you added a new SNS topic in serviceA, and serviceB and serviceC subscribes to the new topic. For the first deployment after the change, you need to deploy serviceA first, and then deploy serviceB and serviceC. Again, if you were to deploy all three services concurrently, serviceB and serviceC will fail for the reason as above.
