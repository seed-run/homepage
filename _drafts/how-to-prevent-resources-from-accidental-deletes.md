# How to prevent resources from accidental deletes?

Look at this concrete example:
```
...
  Resources:
    UsersTable:
      Type: AWS::DynamoDB::Table
      Properties:
        TableName: users
...
```

On a subsequent deployment, if you makes a typo on the TableName, ie. userss, upon deployment the 'users' table will be dropped and a new (and empty) table 'userss' with the same schema will be created.

1. Review update changeset
- serverless deploy runs serverless package to generate artifact and then serverless deploy to deploy the artifact
- run serverless package first, which will generate a CloudFormation template that is going to be deployed
- go into CloudFormation console, select the stack for the service, click on Create Changesset, and upload the template
- you will get a list of actions CloudFormation will perform on your stack if you were to deploy

  Seed does this out of the box. And Seed will also highlight the key changes like removing a DynamoDB table or a SNS subscription. Seed will deploy after you review and confirm the changes. - https://seed.run/docs/promoting-to-production
  ![](https://d33wubrfki0l68.cloudfront.net/ce8af52ceb7d7a209ee5a875886189355f7ae59e/e312f/assets/docs/promoting-to-production/confirm-change-set.png)

1. Keep the resource when the stack is deleted
  By default, the DeletionPolicy for the resources are 'Delete', meaning when the stack is deleted, all it resources are deleted. Set the DeletionPolicy to 'Retain' on the resources. This is especially useful for the resources that contains data. Change the resource definition above to:
  ```
   Resources:
    UsersTable:
      Type: AWS::DynamoDB::Table
      DeletionPolicy: Retain
      Properties:
        TableName: users
  ``` 

1. Prevent the stack being deleted
  Finally, you can prevent users from deleting a stack by enabling termination protection. You can do so in the CloudFormation console:
  ![](https://i.imgur.com/7907NXd.png)
  Alternatively, via AWS CLI:
  ```
  aws cloudformation update-termination-protection –enable-termination-protection –stack-name STACK_NAME
  ```

