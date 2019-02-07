---
layout: docs
title: Adding a Stage
---

Seed supports both [branch based workflow]({% link _docs/working-with-branches.md %}) and [pull request based workflow]({% link _docs/working-with-pull-requests.md %}). In this chapter let's look at how to deploy individual Git branches to different stages.

Create a new branch.

``` bash
$ git checkout -b new-branch
```

Push the branch to remote.

``` bash
$ git push -u origin new-branch
```

Go to Seed console, navigate to your app, hit **Settings**, and **Create a Stage**.

![Click Create a Stage Button](/assets/docs/adding-a-stage/click-create-a-stage.png)

Select a branch (for example, `new-branch`) from the drop down, give it a **Stage Name**, and select **Create Stage**. A default stage name is pre-filled based on the branch name, you can select a different name.

![Select Branch](/assets/docs/adding-a-stage/select-branch.png)

The stage name is used internally while deploying the project via `serverless deploy --stage STAGE_NAME`. The stage name is also used to [configure stage variables]({% link _docs/configuring-stage-variables.md %}). 

Once a stage is created, it is available across all the services in the app.

![New stage added](/assets/docs/adding-a-stage/new-stage-added.png)

You can now click on the stage to take a look at the services deployed in this stage.

![New stage](/assets/docs/adding-a-stage/new-stage.png)

You start the first build for the stage by either hitting **Trigger Deploy** or by pushing a commit to the branch that is linked to the stage.

![Build stage in progress](/assets/docs/adding-a-stage/build-stage-in-progress.png)

If the build is successful and tests pass, all the services get deployed to this stage. At the same time, a verified build is packaged for production. You can read more about this in the [Promoting to production]({% link _docs/promoting-to-production.md %}) chapter.

Once a stage has been added, Seed will automatically create a new build when you `git push` to the update the remote branch.

Finally, you can configure Seed to automatically create and remove stages when a new Git branch is created or removed. You can read more about this in the [Working with Branches chapter]({% link _docs/working-with-branches.md %}).
