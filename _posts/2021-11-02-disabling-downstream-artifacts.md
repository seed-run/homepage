---
layout: post
title: Disabling downstream artifacts
categories: news
author: frank
---

You can now configure Seed to disable generating downstream artifacts.

Seed by default generates some build artifacts for downstream stages. These artifacts are used to generate CloudFormation change sets when promoting. If you are not promoting builds across stages, you can now disable this by adding the following to your Seed build spec.

``` yml
disable_artifacts: true
```

Read more about [creating a build spec]({% link _docs/adding-a-build-spec.md %}) and [promoting to production]({% link _docs/promoting-to-production.md %}) over on our docs.
