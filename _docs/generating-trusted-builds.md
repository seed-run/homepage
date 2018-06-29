---
layout: docs
title: Generating Trusted Builds
---

When Seed builds your Serverless Framework application, it breaks up the `serverless deploy` process into a couple of steps. For example, for a commit to `master`, connected to a stage called `dev` will trigger the following:

1. A package is created for the target stage (in this case `dev`) using the `serverless package` command.
2. A package is created for the production stage.
3. The target stage (in this case `dev`) is deployed using the `serverless deploy --package` command. Here the package is the one generated in Step 1.

The package created in Step 2 of this process is tagged with the Git commit and stored for later use. So when you decide to promote this build to production we simply load up that previously stored package and deploy it using the `serverless deploy --package` command.

This process of storing the package is done to ensure that once a build has been tested and packaged, we simply use that to deploy to the downstream stages. Thereby avoiding any unnecessary surprises when we are building for production at a later date.

Serverless Framework currently does not support parameterized build artifacts and so by building for the downstream stages ensures that Seed generates trusted builds on every single commit.
