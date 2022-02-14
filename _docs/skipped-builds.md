---
layout: docs
title: Skipped Builds
---

Sometimes Seed might skip an entire build or skip building a specific service. This chapter goes over the details of why some builds might have been skipped.

There are 4 reasons why a build or service might have been skipped.

1. **Multiple queued builds**

   If you push a commit while one is currently being deployed, the new commit will queue a build. However, if you push another commit while there's one in the queue; the queued build will be skipped.

2. **Newly added service**

   If you add a newly created service to the pipeline that only exists in a specific branch, Seed will skip deploying that service in the other stages. You can [read more about this here]({% link _docs/adding-a-service.md %}#newly-created-services).

3. **Failed deploy phase**

   If a [deploy phase]({% link _docs/configuring-deploy-phases.md %}) fails, all the services in the following deploy phases will be skipped.

4. **Build minutes limit**

   If your account has reached the build minutes limit, any new commits will result in skipped builds. [Consider upgrading your plan]({% link pricing.html %}) to avoid any disruption.

## Skipping Git Push Deployments

By default if your stages are [configured to auto-deploy]({% link _docs/updating-the-stage-source.md %}), they'll trigger a new deployment for every `git push`. For some commits you might not want to trigger a build. You can do this by including either of these as a part of your commit message.

- `[skip ci]`
- `[ci skip]`

So for example, pushing a commit like the following will not trigger a build.

``` bash
$ git commit -a "[skip ci] removing newline character"
$ git push
```

Note that, unlike the skipped build cases above, these builds will not be reflected on the Seed console.
