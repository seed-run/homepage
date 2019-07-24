# CircleCI vs Travis CI vs CodePipeline vs Seed

## Cost
- Circle/Travis: Expensive. Cost scales with the number concurrent builds. This pricing model gets very expensive quickly when deploying monorepo applications with a many services.
- CodePipeline: Cheapest. Pay per use model. Unlimited concurrency.
- Seed: Cheap. Cost scales with build minutes used. Unlimited concurrency.

## Monorepo support
- CodePipeline/Circle/Travis:
  - no out of the support
  - need custom scripting to only deploy changed services.
- Seed
  - support deploy/promote/rollback individual services in monorepo
  - skip un-changed services

## Easiness to configure
- CodePipeline: HARD.
  - Require configuring multiple AWS services and tying them together. For example, CodeBuild for build process, S3 to store build cache and artifact, CloudWatch to store build logs. Usually takes 2-3 days to setup.
- Circle/Travis: EASIER.
  - A basic pipeline can be configured via a single buildspec.
  - The more services and more environment stages you have, more complicated the buldspec.
  - Need to configure caching for the app and each services.
  - Usually takes half a day to 1 day to setup.
- Seed: EASIEST. 
  - No buildspec required.
  - Auto-detecting services in app.
  - Out of the box support for environment stages and associate stages to AWS accounts.
  - Out of the box dashboard showing the version of each service that is deployed to each stage

## Serverless integration
- Seed: YES
  - picks the default build and deploy scripts outt of the box based on service runtime, no build script required
  - supports multi AWS account deployment out of the box
  - preview CloudFormation changeset on promote
  - view deployed resources
- Circle/Travis: NO
  - manually manage multiple AWS account credentialss in buildspec
- CodePipeline: NO
  - supports multi AWS account deployment out of the box

## DevOp Costs
- CodePipeline: HIGH
  - Adding a new service requires updating the pipeline.
  - Setting up a new stage environment for new feature branch require creating a new pipeline.
- Circle/Travis: LOW
  - Adding a new service requires updating the buildspec.
  - Buildspec can be scriptted to auto track new git branches.
  - Settiing up new AWS account requires updating the git branch to AWS credentials mapping in buildspec.
- Seed: LOWEST
  - New service can be done through the dashboard in less than a minute.
  - New stage environments can be done through the dashboard in less than a minute.
  - New AWS accounts can be linked through the dashboard in less than a minute.

## Pull Request Workflow
- Seed: YES
  - each PR is merged with the base branch and deployed to a PR stage for preview.
  - resources in PR stage is auto-removed on PR close
- Travis: NOT GOOD
  - need to manually remove resources in PR stages on PR close
- Circle: NOT GOOD
  - Can be scripted to perform git merge with base branch in buildspec.
  - need to manually remove resources in PR stages on PR close
- CodePipeline: NO
  - No support for PR
  - Can be achieved by using a Lambda function to listen for PR events from the git provider, and then triggering the pipeline. Requires a lot of setup.

## Feature Branch Workflow
- Seed
  - Feature branches are auto deployed to a feature stage
  - resources in feature stage is auto-removed on branch close
- Travis/Circle: NOT GOOD
  - need to manually remove resources in feature stages on branch close
- CodePipeline: NOT GOOD
  - need to create a pipeline for new branches
  - need to manually remove resources in feature stages on branch close


## When to use Seed
- monorepo app with multiple services
- number of services is growing
- have short-lived environment stages (ie. practicing PR workflow and feature branch workflow)
- would like to have a birdseye view of the pipeline for all services across all stages
- needs manual promote with changeset
- needs rollback

## When to use CircleCI and Travis CI
- do not have many environment stages to manage, or using a separate solution for CD
- 1 service per app, or is paying for enough concurrent capacity to deploy monorepo app
- Serverless is a part of large system with complex test cases, in which case you can use CircleCI/Travis CI in conjunction with Seed. Seed seamlessly integrates with all common CI services, and deploys once CI tests pass.

## When to use CodePipeline
- consolidated billing: 1 bill for all services
- all AWS approach
- If you’re looking for a cheap CI solution, and are willing to put in the work to customize your environment
