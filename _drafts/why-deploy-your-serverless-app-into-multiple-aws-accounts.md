# Why deploy your Serverless app into multiple AWS accounts?

Best-practice is to deploy each environment into a separate AWS accouunt. At least keep Production separate from the rest of the environments ie. Dev, Staging, QA, etc.

Main reason is to protect Production. Here is why:


## Environment separation

Imaging you removed a DynamoDB table or a Lambda function in your `serverless.yml` definition, and intended to deploy it to the Development environment. But instead you deployed it to the Production. Not every developer should have access or direct access from their terminal to the Production environment. If all environments are in the same AWS account, you need to carefully craft a detailed IAM policy to restrict/grant which resources a user can access for which environment. It is very hard.

By keeping each environment in a separate account, you can manage user access on an account by account basis. And the user can simply have AdministratorAccess access to the accounts he has access to.


## Resource Limits
- AWS has various hard limits and soft limits per account. For example: Lambda code storage size; # of S3 buckets; # of concurrent Lambda execution.
- Ensure non-production resources not taking up limit and causing builds to fail.


## Consolidated Billing

- Having seaparate accounts for your environments is recommended by AWS. In AWS Organizations console, you can view and manage all the AWS accounts in your root account.
- You don't have to setup billing details for each account. Billing is consolidated to the main account.
- You can see a breakdown of usage and cost for each service in each account.
