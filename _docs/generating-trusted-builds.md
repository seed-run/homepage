---
layout: docs
title: Generating Trusted Builds
---

When Seed builds your Serverless Framework application, it generates some build artifacts as a part of the build process. These artifacts are stored for later use. In this chapter we'll look at them in a bit more detail.

![Build artifacts in Seed](/assets/docs/generating-trusted-builds/build-artifacts-in-seed.png)

Seed splits up the `serverless deploy` process into a couple of steps. For example, for a commit to `master`, connected to a stage called `dev` will trigger the following:

1. A package is created for the target stage (in this case `dev`) using the `serverless package` command.
2. A package is created for the production stage (and [a pre-production stage]({% link _docs/editing-the-pipeline.md %}#add-a-staging-or-pre-production-stage), if configured).
3. The target stage (in this case `dev`) is deployed using the `serverless deploy --package` command. Here the package is the one generated in Step 1.

The package created in Step 2 of this process is tagged with the Git commit and stored for later use. So when you decide to promote this build to production, we load up that previously stored package and use that to generate a [CloudFormation Change Set](https://aws.amazon.com/blogs/aws/new-change-sets-for-aws-cloudformation/). Step 2 is also carried out asynchronously and it doesn't count towards your build minutes.
