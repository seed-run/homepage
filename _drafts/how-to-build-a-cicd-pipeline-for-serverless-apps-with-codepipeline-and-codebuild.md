---
layout: post
title: How to build a CI/CD pipeline for Serverless apps with AWS CodePipeline and CodeBuild
image: assets/social-cards/serverless-cicd-codepipeline-codebuild.png
description: In this post we'll look at how to configure a CI/CD pipeline for a Serverless app with AWS CodePipeline and CodeBuild. We'll be using a real-world monorepo Serverless app that'll be deployed to separate development and production AWS accounts. We'll set up a PR based Git workflow and remove our services once the PRs are merged. 
categories: tips
author: frank
---

In one of our [previous posts we looked at how to build a CI/CD pipeline for Serverless apps on AWS with CircleCI]({% link _posts/2019-07-09-how-to-build-a-cicd-pipeline-for-serverless-apps-with-circleci.md %}). Today, we'll look at how to do the same with [AWS CodePipeline](https://aws.amazon.com/codepipeline/) and [AWS CodeBuild](https://aws.amazon.com/codebuild/). The purpose of these posts is to dive deep into real-world CI/CD setups, something which most of the tutorials out there skip. We'll try to illustrate how to set up something similar to [Seed](/) but using CodePipeline and CodeBuild instead. It'll also give a you chance to see how Seed makes your life easier!

To cover a real-world setup we'll be using a:

- A monorepo Serverless app
- With multiple services
- Deployed to separate development and production AWS accounts

As a refresher, a monorepo Serverless app is one where multiple Serverless services are in subdirectories with their own `serverless.yml` file. Here is [a sample repo for the app that we'll be configuring](https://github.com/seed-run/serverless-example-monorepo-with-codepipeline-codebuild). The directory structure might look something like this:

```
/
  package.json
  services/
    users-api/
      package.json
      serverless.yml
    posts-api/
      package.json
      serverless.yml
    cron-job/
      package.json
      serverless.yml
```

### What we'll be covering

1. How to deploy your monorepo Serverless app on Git push
2. How to deploy to multiple AWS accounts
3. How to deploy using the pull request workflow
4. How to clean up unused branches and closed pull requests

Note that, this guide is structured to work in standalone steps. So if you only need to get to be able to deploy to multiple AWS accounts, you can stop after step 2.

### Pre-requisites

- A monorepo Serverless app in a GitHub repo. Head over to our [template repo](https://github.com/seed-run/serverless-template-monorepo) and click on **Use this template** to clone it to your account.

![Use Seed monorepo Serverless GitHub template](https://d33wubrfki0l68.cloudfront.net/0d9d4d964139682f8b5cf2f53666725a2eb51c3a/3e8df/assets/blog/how-to-build-a-cicd-pipeline-for-serverless-apps-with-circleci/use-seed-monorepo-serverless-github-template.png)

### 1. How to deploy your monorepo app on Git push

Let's first create an IAM role which we will use later to deploy our Serverless app. Head over to your AWS IAM console, and select **Roles** on the left.
![](https://i.imgur.com/MB9p4sR.png)

Select **Create role**; select **CodeBuild** from the list of services; then select **Next: Permissions**
![](https://i.imgur.com/7bp6Xf4.png)

Check **AdministratorAccess** and select **Next: Tags**
![](https://i.imgur.com/GlKmFt0.png)

Select **Next: Review**, name the role **CodeBuildRole**, and then select **Create role**
![](https://i.imgur.com/SVZ4Wpx.png)


Now, let's create our pipeline. Head over to your AWS CodePipeline console, and select **Create pipeline**
![](https://i.imgur.com/2lsrYQ7.png)

Name the pipeline **master** since we are going to configure this pipeline to deploy on git pushes to the **master** branch. Select **Next**.
![](https://i.imgur.com/JUXFXWh.png)

Select **GitHub** as the source provider. After connecting your GitHub account, select your repository and the **master** branch. Then select **Next**.
![](https://i.imgur.com/WPhFCWz.png)

Select **AWS CodeBuild** as the Build provider, and select **Create project**.
![](https://i.imgur.com/bVLuP63.png)

In the new window, we are going to create a CodeBuild project to deploy our first Serverless service.

Enter **deploy-users-api** as the project name.
![](https://i.imgur.com/eZidPdf.png)

Scroll down to the **Environment** section. Select **Ubuntu** operating system; **Standard** runtime; and **aws/codebuild/standard:2.0** image.
![](https://i.imgur.com/whbBNmk.png)

Scroll down and select **Existing service role**. Pick the **CodeBuildRole** we created.
![](https://i.imgur.com/fRXjFHO.png)

Expand **Additional configuration**. Add an environment variable with:
- Name: **SERVICE_PATH**
- Value: **services/users-api**

![](https://i.imgur.com/uZ8EPMi.png)

Scroll to the bottom and select **Continue to CodePipeline** to finish creating the CodeBuild project and continue with creating our pipeline.

The **Project name** field should be autofilled with the CodeBuild project we just created. Select **Next**.
![](https://i.imgur.com/41gODMT.png)

Select **Skip deploy stage**, and confirm **Skip**.
![](https://i.imgur.com/bhv0b6H.png)

Scroll to the bottom and select **Create pipeline**.
![](https://i.imgur.com/GuD4FVy.png)

After the pipeline is created, it automatically deploys the latest commit. The **Build** stage will fail since we have not told CodeBuild how to build and deploy our Serverless service yet. We will do that in a sec.
![](https://i.imgur.com/6DqGHaC.png)

Before that, let's create two more CodeBuild projects to deploy our **posts-api** and **cron-job** services.

Select **Edit** at the top. Then select **Edit stage** for the **Build** stage at the bottom. Then select **+  Add action**.
![](https://i.imgur.com/RanlgRD.png)

Fill the form:
- Action name: **DeployPostsApi**
- Action provider: **AWS CodeBuild**
- Input artifact: **SourceArtifact**

Then select **Create project**.
![](https://i.imgur.com/MVM3Kus.png)


Repeat the same steps to create a CodeBuild project named **deploy-posts-api** with the same configuration. Only difference is make sure environment variable set to:
- Name: **SERVICE_PATH**
- Value: **services/posts-api**

After the action is created, your pipeline should look like
![](https://i.imgur.com/QBe1gJd.png)

Select **+ Add action** again and create a new action named **DeployCronJob**. Name the CodeBuild project **deploy-cron-job** with environment variable:
- Name: **SERVICE_PATH**
- Value: **services/cron-job**

To keep naming consistent, rename the **Build** action to **DeployUsersApi**. Now the pipleline should look like
![](https://i.imgur.com/ACxOr9G.png)

Scroll up and select **Save** and confirm.

Go to the cloned repository and click on **Create new file**.

![Create new file in cloned GitHub repo](https://d33wubrfki0l68.cloudfront.net/9e001b8409492bd8e9ddd3845d94f2d664e7d691/478be/assets/blog/how-to-build-a-cicd-pipeline-for-serverless-apps-with-circleci/create-new-file-in-cloned-github-repo.png)

Name the new file `buildspec.yml` and paste the following:

{% raw %}
``` yaml
version: 0.2

phases:
  install:
    runtime-versions:
      nodejs: 10
    commands:
      - npm install -g serverless
      - npm install
      - cd ${SERVICE_PATH} && npm install && cd -
  build:
    commands:
      - cd ${SERVICE_PATH} && serverless deploy -s ${CODEBUILD_INITIATOR##*/} && cd -

cache:
  paths:
    - node_modules
    - ${SERVICE_PATH}/node_modules
```
{% endraw %}

Let's quickly go over what we are doing here:
  - We created a build template that will reads the **path of a service** from the environment variables we set earlier.
  - The build job will run 3 times, once for each service.
  - The build job does an `npm install` in the repo's root directory and in the service subdirectory.
  - The build job then goes into the service directory and runs `serverless deploy` using the pipeline name (also the branch name) as the stage name.
  - As a side note, we also specified that we want to cache the `node_modules/` directory in both the root and the service directory for faster deployment.

Next, scroll to the bottom and click **Commit new file**.

Back in CodePipeline, you will see the pipeline is currently running.

![View-running-jobs-in-CodePipeline](https://i.imgur.com/NZffIHu.png)

Click on **Details** for the DeployUsersApi action. You will see the output for each of the commands in our buildspec. Scroll down, and you should see the output for the `serverless deploy -s master` command.
![View-build-logs-in-CodeBuild-and-CodePipeline](https://i.imgur.com/xEfJAnF.png)

Now that we have the basics up and running, let's look at how to deploy our app to multiple AWS accounts.


### 2. How to deploy to multiple AWS accounts

You might be curious as to why we would want to deploy to multiple AWS accounts. It's a good practice to keep your development and production environments in separate accounts. By separating them completely, you can secure access to your production environment. This will reduce the likelihood of accidentally removing resources from it while developing.

Assume we have been operating in the Production account (ie. account id **111111111111**); and you have another AWS account you use for Staging(ie. account id **222222222222**). We are going to configure git pushing to the **staging** branch auto deploys to this Staging account.

First, let's create an IAM role that grants the Production account permission to deploy to the Staging AWS account. Go to the AWS IAM console in your Staging account, select **Roles** on the left menu and select **Create role**.

Select **Another AWS Account** at the top and enter the account id for the Production account. Then select **Next: Permissions**
![](https://i.imgur.com/aKOW9Bb.png)

Select **AdministratorAccess** and select **Next: Tags**
![](https://i.imgur.com/y4FYmRd.png)

Select **Next: Review**. Name the role **CodeBuildRole**. Select **Create role**.
![](https://i.imgur.com/wlk3Lr5.png)

Select the role just created, and take a note of the **Role ARN: arn:aws:iam::222222222222:role/CodeBuildRole** which we will use next.
![](https://i.imgur.com/GtLRGxB.png)

Go back to the Production AWS account. Go to CodePipeline console and select **Create pipeline**. This time, we will create a **staging** pipeline. Then select **Next**.
![](https://i.imgur.com/eUKkXvN.png)

Select the same GitHub repository, but this time enter **staging** branch. Select **Next**. If you have not created a **staging** branch, quickly go to your Github repo and create one.
![](https://i.imgur.com/1AlNPbu.png)

Select **AWS CodeBuild** and select the **deploy-users-api** CodeBuild project we created previously. Select **Next**.
![](https://i.imgur.com/ScYnYeZ.png)

Select **Skip deploy stage** and finally select **Create pipeline**.

Now, a pipeline is created, and it will get triggered on git push to the **staging** branch. Again, the pipeline auto-deploys the latest commit in the **staging** branch upon the pipeline creation. But first, let's finish configuring the pipeline.

Select **Edit**, and perform:
- Add **DeployPostsApi** action;
- Add **DeployCronJob** action; and
- Rename **Build** to **DeployUsersApi** action

Select **Save** to apply the edit. 

Go to your GitHub repo and open `buildspec.yml` in the **staging** branch. Replace it with the following:

{% raw %}
``` yaml
version: 0.2

phases:
  install:
    runtime-versions:
      nodejs: 10
    commands:
      - npm install -g serverless
      - npm install
      - cd ${SERVICE_PATH} && npm install && cd -
  build:
    commands:
      - STAGE_NAME=${CODEBUILD_INITIATOR##*/}
      - |
        if [ "${STAGE_NAME}" = "staging" ]; then
          CRED=`aws sts assume-role --role-arn arn:aws:iam::222222222222:role/CodeBuildRole --role-session-name prod-access`
          echo $CRED
          AWS_ACCESS_KEY_ID=`node -pe 'JSON.parse(process.argv[1]).Credentials.AccessKeyId' "$CRED"`
          AWS_SECRET_ACCESS_KEY=`node -pe 'JSON.parse(process.argv[1]).Credentials.SecretAccessKey' "$CRED"`
          AWS_SESSION_TOKEN=`node -pe 'JSON.parse(process.argv[1]).Credentials.SessionToken' "$CRED"`
          AWS_EXPIRATION=`node -pe 'JSON.parse(process.argv[1]).Credentials.Expiration' "$CRED"`
        fi
        cd ${SERVICE_PATH} && serverless deploy -s ${STAGE_NAME} && cd -

cache:
  paths:
    - node_modules
    - ${SERVICE_PATH}/node_modules
```
{% endraw %}

This does a couple of things:
  - A git push to the **staging** branch will be trigger the **staging** pipeline. And CodeBuild will assume into the Staging AWS account and get a temporary AWS credentials. CodeBuild then uses these temporary credentials to deploy.
  - A git push to the **master** branch will still be deployed to the Production account.

Commit and push this change. This will trigger CodePipeline and CodeBulid to build the **staging** branch. This time deploying to your Staging account.

And that's it! Let's wrap things up next.

#### Next steps

It took us a few steps but we now have a fully-functional CI/CD pipeline for our monorepo Serverless app. It supports a PR based workflow and even cleans up once a PR is merged. The repo used in this guide is available [here with the complete CodeBuild configs](https://github.com/seed-run/serverless-example-monorepo-with-codepipeline-codebuild).

Some helpful next steps would be to auto-create custom domains for your API endpoints, send out Slack or email notifications, generate CloudFormation change sets and add a manual confirmation step when pushing to production, etc. You also might want to design your workflow to accommodate for any dependencies your services might have. These are cases where the output from one service is use in another. 

Finally, if you are not familiar with [Seed](/), it's worth noting that it'll do all of the above for you out of the box! And you don't need to write up a build spec or do any scripting.
