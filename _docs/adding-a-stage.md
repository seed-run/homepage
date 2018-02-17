---
layout: docs
title: Adding a Stage
---

Seed supports both branch based workflow and [pull request based workflow]({% link _docs/working-with-pull-requests.md %}). With branch based workflow, Seed allows you to deploy individual Git branches to different stages.

Create a new branch.

``` bash
$ git checkout -b new-branch
```

Push the branch to remote.

``` bash
$ git push -u origin new-branch
```

Go to Seed console, navigate to your project and select **Add Stage**.

![Add Stage](/assets/docs/adding-a-stage/add-stage.png)

Select `new-branch` from the drop down, give it a **Stage Name**, and select **Add Stage**. A default stage name is pre-filled based on the branch name, you can select a different name.

![Select Branch](/assets/docs/adding-a-stage/select-branch.png)

The stage name is used internally while deploying the project via `serverless deploy --stage STAGE_NAME`. The stage name is also used to [configure stage variables]({% link _docs/configuring-stage-variables.md %}). 

When a new stage is created, Seed triggers a build automatically.

![Build Stage](/assets/docs/adding-a-stage/build-stage.png)

If the build is successful and tests pass, the stage gets deployed. At the same time, a verified build is packaged for production. You can read more about this in the [Promoting to production]({% link _docs/promoting-to-production.md %}) chapter.

![Build Stage Successful](/assets/docs/adding-a-stage/build-stage-success.png)

Seed automatically creates a new build for the stage when you `git push` to the update the remote branch.
