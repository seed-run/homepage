---
layout: post
title: Service path in the build spec
categories: news
author: jack
---

You can now access the service paths in the build spec. We added two new environment variables to our build environments.

1. `$SEED_SERVICE_PATH`: The path of the service as set in the service's settings. For example, `/services/posts`. If the service is at the root of the repo, this value is empty.
2. `$SEED_SERVICE_FULLPATH`: The absolute path of the service inside the build container. For example, `/tmp/seed/source/services/posts`.

[Read more about the build spec and the other built-in environment variables here]({% link _docs/adding-a-build-spec.md %}#build-environment-variables).
