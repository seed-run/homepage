# How to deploy only changed services in a monorepo Serverless app?

In a single-service Serverless app, the deployment strategy is straight forward: deploy my app on every git push.

However, in a monorepo setup, an app is made up of many Serverless services. We have seen teams manage over 40 services in a single repo on Seed, and that number keeps going up as teams continue to work on their app. Now, when you fix a typo in one of your services, do you want to deploy all other services?

That answer is no for many teams. And there are two main reasons:

- Slow: deploying all services can take very long, especially when you are not deploying them concurrently.
- Expensive: traditional CI services charge for concurrency, ie. it costs $50 for each added concurrency on CircleCI, hence it can be very costly to deploy all services concurrently.

## Strategy 1: Skipping deploying in Serverless Framework

The `serverless deploy` command has built-in support to skip a deployment if the deployment package is not changed. A bit of background, when you run `serverless deploy`, two things are done behind the scene. It first does a `serverless package` to generate a deployment package including the CloudFormation template and the zipped Lambda code; then it does a `serverless deploy -p path/to/package` to deploy the package that was created. Before Serverless deploys the package in the second step, it first computes the hash of the package and compares with that of the previous deployment. If same, the deployment is skipped.

However, there are two downside to this:

- Serverless still has to generate the deployment package first. For a NodeJS application, this could mean installing the dependencies, linting, webpacking, and finally packaging the code.
- If the previous deployment failed due to an external cause, after you fix the issue and re-run `serverless deploy`, the deployment will be skipped. For example, you tried to create an S3 bucket in your 'serverless.yml', but you hit the 100 S3 buckets per account limit. You talked to AWS support and had the limit lifted. Now you re-run `serverless deploy` , but since neither the CF template or the Lambda code changed, the deployment will be skipped.

## Strategy 2: Check the Git log for changes

Let's consider the following monorepo setup as an example. The app has two Serverless Framework services, located inside the services/ folder. And the libs/ folder contains code that is shared between the services.

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

When a the code is pushed, you can get a list of changed files since the previous deployment by running `git diff --name-only ${prevCommitSHA} ${currentCommitSHA}`. With the list of changed files, there are 3 scenarios that can happen:

1. file changed in services/serviceA ⇒ deploy serviceA;
2. file changed in services/serviceB ⇒ deploy serviceB;
3. file changed in libs/ ⇒ deploy serviceA and serviceB.

Your repo setup can look different, but the general concept hold true. You have to figure out which file changes affect an individual service, and which affect all. The advantage of this strategy is that you know upfront which services can be skipped.

The folder structure laid out in the example above is the monorepo setup Seed recommend. It is clean and scales well as the number of services increase. And if you follow this setup, Seed can automatically figure out the changed services and only deploy those changed. You can read more here - [https://seed.run/docs/deploying-monorepo-apps](https://seed.run/docs/deploying-monorepo-apps)

## Conclusion

There is no harm to use both strategies together. Check the changed files manually, and when unsure, fallback to let Serverless generate the deployment package and check the hash.
