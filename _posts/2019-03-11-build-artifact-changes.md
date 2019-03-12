---
layout: post
title: Build Artifact Changes
author: jack
---

Seed generates build artifacts that it uses to create Change Sets (to confirm promotions) and while rolling back. We made a couple of changes to how these artifacts are generated.

![Build artifacts in report panel](/assets/blog/build-artifact-changes/build-artifacts-in-report-panel.png)

Build artifacts are now displayed clearly as a part of the build report panel. This gives you a good overview of the entire build process, without having to dig deep into the various build steps.

![Build artifacts in Seed](/assets/blog/build-artifact-changes/build-artifacts-in-seed.png)

You can also view the status of all the build artifacts as a whole.

Build artifacts also don't affect the status of the build. Meaning that the build is still marked as complete even if the artifacts have failed to generate. This change ends up being necessary since you might have cases where the artifact for a certain stage fails because you haven't configured the resources for the stage yet. Note that, if the build artifacts are missing, it doesn't affect the rest of the build process (promoting or rolling back). You can read more on the [Seed build process in our docs]({% link _docs/generating-trusted-builds.md %}).

An added advantage of this change is that your builds won't wait for the artifact generation process to complete. This means that your builds in Seed just got a little faster! Just another way Seed is making sure you have a great deployment experience for your Serverless Framework apps on AWS.
