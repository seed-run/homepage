# How to deploy your Serverless app into multiple AWS accounts?

## Why?
Teams commonly have multiple AWS accounts that they use for different environments. To understand why need to deploy into multiple AWS accounts, read this doc - https://...

## How to do it with Serverless?

- Serverless made it easy via stages.
- Treat a stage as an environment.
- Deploy each stage into a separate account using different AWS profiles.
- Serverless uses CloudFormation behind the scene to provision AWS resources. The CF template is generated from your serverless.yml.
- Since the same serverless.yml is used to generated the CF template for all stages, the resources provisioned for the stages are identical mirrors of one another.
- This allows Development, QA, Testing and Staging environments be able to mirror the Production environment as much as possible

## How to customize a stage
- Not all resources need to be deployed to all stages. Ie. you might not need a DAX caching layer for your DynamoDB tables in development stages. You can have optional resources for a specific stage. 
https://github.com/seed-run/serverless-example-monorepo-with-conditional-resources

## Watch out for thrashed naming:
- For resources require globally unique naming across AWS accounts (like S3), ensure to parameterize the resource naming so resources in different stages do not thrash.
- Also if you plan to deploy multiple stages into the same AWS account (ie. all development stages in the same accouont), ensure to parameterize as well.

## Watch out for account limits:
- Newly created AWS accounts have a lower limit for certain services. For example, AWS Codebuild has a default limits of 20 maximum number of concurrent running builds. For a new account, the limit is 1.
- Need to ensure the new account's service limit meets requirement. And contact AWS support to raise the limit otherwise.

## Watch out for un-usesd resources in orphan account:
- AWS provides consolidated billing across all your the accounts in your AWS Organization. You can see a breakdown on the cost per account per service. You can identify and remove un-used resources.
- Also, removing an account automatically de-provision all the resources provisioned in the accouont.
