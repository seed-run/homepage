---
layout: post
title: Deploying newly created services
categories: news
author: jack
---

We recently rolled out an update to fix the way Seed handles deploying services that only exist in a specific stage.

![Skipped build in Seed pipeline](/assets/blog/deploying-newly-created-services/skipped-build-in-seed-pipeline.png)

Services in Seed are added across all the stages in the pipeline. However, there might be cases where your newly created service only exists in a specific branch. For example, in the screenshot above, the _users_ service only exists in the `master` branch that's tied to the dev stage. In this case, builds in other stages would fail because Seed would not be able to find and deploy this service.

![Skipped service build log](/assets/blog/deploying-newly-created-services/skipped-serivce-build-log.png)

We rolled out an update to fix this. Seed will now skip these newly added services. This will allow you to continue deploying the rest of your pipeline while the service is still being worked on.

You can read more about this [over on our docs on adding a service]({% link _docs/adding-a-service.md %}#newly-created-services).
