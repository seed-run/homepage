# How to setup git workflow for your Serverless app?

A couple of fundamental uniqueness for Serverless:
1. Because it is free (Lambda, API Gateway, DynamoDB) and easy (infrastructure as code) to replicating a stack at scale, you can have many dev environments mirroring the production.
2. With Serverless, you are deploying both Code and Infrastructure. Infrastructure changes are not always (easily) reversible. Need to be extra careful releasing changes to production.


## Feature Branch Workflow
- a stage environment is created on branch creation
- the stage is usually named after the name of the feature branch
- when commits are pushed to the feature branch, they are deployed to the feature stage
- hence each feature branch has a complete stack and API endpoint (if it had one) to test with.
- remove the stage on branch deletion
- results in many short-lived branches
- remove the deployed resources from your AWS account (traditional CI systems do not usually monitor branch deletion, Seed does this out of the box)

## PR Workflow
- a stage environment is created on each PR creation
- the stage is usually named after the pull request number ie. 'pr257'
- when commits are added to the pull request, temporarily merge the source branch and the upstream branch, and deploy the merged version to the pr stage.
- hence each pull request has a complete stack and API endpoint (if it had one) to test with.
- removed the stage on PR close
- results in many short-lived branches
- remove the deployed resources from your AWS account (traditional CI systems do not usually monitor branch deletion, Seed does this out of the box)

## Pure Git Workflow
- 'master' branch auto deploys to the Production
- work in dev branches, commits never made directly in the 'master' branch
- when releasing to production, merge commits into 'master'

## Manual Approval Workflow
- Development environments are auto-deployed from a git branch
- Production environment is not auto-deployed to
- when releasing to production, review the code diff
- Also generate a CloudFormation changeset between what is currently running in the Production and what is about to be deployed. And review the changeset.
- Confirm the changes and proceeds with the release.
