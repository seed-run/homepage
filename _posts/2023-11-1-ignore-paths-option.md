---
layout: post
title: Ignore Paths Option
categories: news
author: frank
---

Seed now lets you ignore a list of paths in your repo. Changes to these paths will not trigger a deployment.

For large monorepos with multiple applications, it might make sense to not trigger a build in Seed if an unrelated file or directory changes on `git push`. To ignore these paths you can now use the [`ignore_paths`]({% link _docs/adding-a-build-spec.md %}#ignoring-code-changes) option in your [build spec]({% link _docs/adding-a-build-spec.md %}).

```yml
ignore_paths:
  - docs/**
  - README.md
```

Note that, in the above example a build is skipped only if the file paths match every path in the `ignore_paths` list. [Read more about this over on our docs]({% link _docs/adding-a-build-spec.md %}#ignoring-code-changes).
