---
layout: post
title: How to build a CI/CD pipeline for Serverless apps with CircleCI
image: assets/social-cards/serverless-cicd-circle.png
description: In this post we'll look at how to configure a CI/CD pipeline for a Serverless app with CircleCI. We'll be using a real-world monorepo Serverless app that'll be deployed to separate development and production AWS accounts. We'll set up a PR based Git workflow and remove our services once the PRs are merged. 
categories: tips
author: frank
---

At [Seed](/), we've built a fully managed CI/CD pipeline for [Serverless Framework](https://serverless.com) apps on AWS. So you can imagine we have quite a bit of experience with the various CI/CD services.

Over the next few weeks we are going to dive into some of the most popular services out there. We'll take a detailed look at what it takes to run your own CI/CD pipeline for Serverless apps. This'll give you a good feel for not just how things work but how Seed makes your life easier!

Today we'll be looking at [CircleCI](https://circleci.com). You might have come across tutorials that help you set up a CI/CD pipeline for Serverless on Circle. However, most of these are way too simplistic and don't talk about how to deploy large real-world Serverless apps.

Instead we'll be working with a more accurate real-world setup comprising of:

- A monorepo Serverless app
- With multiple services
- Deployed to separate development and production AWS accounts

As a refresher, a monorepo Serverless app is one where multiple Serverless services are in subdirectories with their own `serverless.yml` file. Here is [the repo of the app that we'll be configuring](https://github.com/seed-run/serverless-example-monorepo-with-circleci) you can refer to. The directory structure might look something like this:

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

Note that, this guide is structured to work in standalone steps. If you only want to deploy to multiple AWS accounts, you can stop after step 2.

Also, worth mentioning that while this guide is helping you create a fully-functional CI/CD pipeline for Serverless; all of these features are available in [Seed](/) without any configuration or scripting.

### Pre-requisites

- A [CircleCI account](https://circleci.com).
- AWS credentials (Access Key Id and Secret Access Key) of the AWS account you are going to deploy to. Follow [this guide](https://serverless-stack.com/chapters/create-an-iam-user.html) to create one.
- A monorepo Serverless app in a GitHub repo. Head over to our [template repo](https://github.com/seed-run/serverless-template-monorepo) and click on **Use this template** to clone it to your account.

![Use Seed monorepo Serverless GitHub template](/assets/blog/how-to-build-a-cicd-pipeline-for-serverless-apps-with-circleci/use-seed-monorepo-serverless-github-template.png)

### 1. How to deploy your monorepo app on Git push

Let's start by configuring the Circle side of things.

Go into your [CircleCI account](https://circleci.com). Select **Contexts** from the left menu, and click **Create Context**.

![Create CircleCI Context](/assets/blog/how-to-build-a-cicd-pipeline-for-serverless-apps-with-circleci/create-circleci-context.png)

Create a context called **Development**.

![Create CircleCI Context called Development](/assets/blog/how-to-build-a-cicd-pipeline-for-serverless-apps-with-circleci/create-circleci-context-called-development.png)

Go in to the **Development** context, and click on **Add Environment Variable**.

![Add Environment Variable in CircleCI](/assets/blog/how-to-build-a-cicd-pipeline-for-serverless-apps-with-circleci/add-environment-variable-in-circleci.png)

Create an variable with:

  - Name: **AWS_ACCESS_KEY_ID**
  - Value: Access Key Id of the IAM user

![Add AWS Access Key Id as Environment Variable in CircleCI](/assets/blog/how-to-build-a-cicd-pipeline-for-serverless-apps-with-circleci/add-aws-access-key-id-as-environment-variable-in-circleci.png)

Repeat the previous step and create another variable with:

  - Name: **AWS_SECRET_ACCESS_KEY**
  - Value: Secret Access Key of the IAM user

![Add AWS Secret Access Key as Environment Variable in CircleCI](/assets/blog/how-to-build-a-cicd-pipeline-for-serverless-apps-with-circleci/add-aws-secret-access-key-as-environment-variable-in-circleci.png)

Go to the cloned repository and click on **Create new file**.

![Create new file in cloned GitHub repo](/assets/blog/how-to-build-a-cicd-pipeline-for-serverless-apps-with-circleci/create-new-file-in-cloned-github-repo.png)

Name the new file `.circleci/config.yml` and paste the following:

{% raw %}
``` yaml
version: 2.1

jobs:
  deploy-service:
    docker:
      - image: circleci/node:8.10
    parameters:
      service_path:
        type: string
      stage_name:
        type: string
    steps:
      - checkout

      - restore_cache:
          keys:
            - dependencies-cache-{{ checksum "package-lock.json" }}-{{ checksum "<< parameters.service_path >>/package-lock.json" }}
            - dependencies-cache

      - run:
          name: Install Serverless CLI
          command: sudo npm i -g serverless
            
      - run:
          name: Install dependencies
          command: |
            npm install
            cd << parameters.service_path >>
            npm install

      - run:
          name: Deploy application
          command: |
            cd << parameters.service_path >>
            serverless deploy -s << parameters.stage_name >>

      - save_cache:
          paths:
            - node_modules
            - << parameters.service_path >>/node_modules
          key: dependencies-cache-{{ checksum "package-lock.json" }}-{{ checksum "<< parameters.service_path >>/package-lock.json" }}

workflows:
  build-deploy:
    jobs:
      - deploy-service:
          name: Deploy Users API
          service_path: services/users-api
          stage_name: ${CIRCLE_BRANCH}
          context: Development
          
      - deploy-service:
          name: Deploy Posts API
          service_path: services/posts-api
          stage_name: ${CIRCLE_BRANCH}
          context: Development
          
      - deploy-service:
          name: Deploy Cron Job
          service_path: services/cron-job
          stage_name: ${CIRCLE_BRANCH}
          context: Development
```
{% endraw %}

Let's quickly go over what we are doing here:
  - We created a job called **deploy-service**, that takes the **path of a service** and the **name of the stage** you want to deploy to. The name of the stage will be used as the `--stage` in the Serverless commands.
  - The **deploy-service** job does an `npm install` in the repo's root directory and in the service subdirectory.
  - The job then goes into the service directory and runs `serverless deploy` with the stage name that's passed in.
  - We also created a workflow that runs the **deploy-service** job for each service, while passing in the **branch name** as the stage name.
  - As a side note, we also specified that we want to cache the `node_modules/` directory in both the root and the service directory for faster deployment.

Next, scroll to the bottom and click **Commit new file**.

Back in Circle, select **ADD PROJECTS** from the left menu, and click on the **Set Up Project** button next to your project. Make sure the **Show forks** checkbox is checked.

![Set Up Project in CircleCI](/assets/blog/how-to-build-a-cicd-pipeline-for-serverless-apps-with-circleci/set-up-project-in-circleci.png)

Select **Linux** as the Operating System, and **Node** as the Language. Go to step 5 and click on **Start building**.

Then click on **WORKFLOWS** in the left menu.

![Click on Workflows in CircleCI](/assets/blog/how-to-build-a-cicd-pipeline-for-serverless-apps-with-circleci/click-on-workflows-in-circleci.png)

Click on the workflow, you will see the 3 jobs that are currently running.

![View Workflow in CircleCI](/assets/blog/how-to-build-a-cicd-pipeline-for-serverless-apps-with-circleci/view-workflow-in-circleci.png)

Click on a job. You will see the output for each of the steps. Scroll down to the **Deploy application** section, and you should see the output for the `serverless deploy -s master` command.

![View build logs in CircleCI](/assets/blog/how-to-build-a-cicd-pipeline-for-serverless-apps-with-circleci/view-build-logs-in-circleci.png)

Now that we have the basics up and running, let's look at how to deploy our app to multiple AWS accounts.


### 2. How to deploy to multiple AWS accounts

You might be curious as to why we would want to deploy to multiple AWS accounts. It's a good practice to keep your development and production environments in separate accounts. By separating them completely, you can secure access to your production environment. This will reduce the likelihood of accidentally removing resources from it while developing.

To deploy to another account, repeat the earlier step of creating a **Development** context, and create a **Production** context with the AWS Access Key Id and Secret Access Key of your production AWS account.

![Create Production Context in CircleCI](/assets/blog/how-to-build-a-cicd-pipeline-for-serverless-apps-with-circleci/create-production-context-in-circleci.png)

Go to your GitHub repo and open `.circleci/config.yml`. Replace it with the following:

{% raw %}
``` yaml
version: 2.1

jobs:
  deploy-service:
    docker:
      - image: circleci/node:8.10
    parameters:
      service_path:
        type: string
      stage_name:
        type: string
    steps:
      - checkout

      - restore_cache:
          keys:
            - dependencies-cache-{{ checksum "package-lock.json" }}-{{ checksum "<< parameters.service_path >>/package-lock.json" }}
            - dependencies-cache

      - run:
          name: Install Serverless CLI
          command: sudo npm i -g serverless
            
      - run:
          name: Install dependencies
          command: |
            npm install
            cd << parameters.service_path >>
            npm install

      - run:
          name: Deploy application
          command: |
            cd << parameters.service_path >>
            serverless deploy -s << parameters.stage_name >>

      - save_cache:
          paths:
            - node_modules
            - << parameters.service_path >>/node_modules
          key: dependencies-cache-{{ checksum "package-lock.json" }}-{{ checksum "<< parameters.service_path >>/package-lock.json" }}

workflows:
  build-deploy:
    jobs:
      # non-master branches deploys to stage named by the branch
      - deploy-service:
          name: Deploy Users API
          service_path: services/users-api
          stage_name: ${CIRCLE_BRANCH}
          context: Development
          filters:
            branches:
              ignore: master

      - deploy-service:
          name: Deploy Posts API
          service_path: services/posts-api
          stage_name: ${CIRCLE_BRANCH}
          context: Development
          filters:
            branches:
              ignore: master

      - deploy-service:
          name: Deploy Cron Job
          service_path: services/cron-job
          stage_name: ${CIRCLE_BRANCH}
          context: Development
          filters:
            branches:
              ignore: master

      # master branch deploys to the 'prod' stage
      - deploy-service:
          name: Deploy Users API
          service_path: services/users-api
          stage_name: prod
          context: Production
          filters:
            branches:
              only: master

      - deploy-service:
          name: Deploy Posts API
          service_path: services/posts-api
          stage_name: prod
          context: Production
          filters:
            branches:
              only: master

      - deploy-service:
          name: Deploy Cron Job
          service_path: services/cron-job
          stage_name: prod
          context: Production
          filters:
            branches:
              only: master
```
{% endraw %}

This does a couple of things:
  - A Git push to the **master** branch will be deployed to the **prod** stage, instead of the stage with the branch name. It'll also use the **Production** context.
  - A Git push to all the other branches will be deployed to the stage with their branch name using the **Development** context.

Commit and push this change. This will trigger Circle to build the **master** branch again. This time deploying to your production account.

Next, let's look at implementing the PR aspect of our Git workflow.

### 3. How to deploy in pull request workflow

A big advantage of using Serverless is how easy and cost effective it is to deploy many different versions (ie. stages) of your app. A great use case for this is to deploy a version of your app for each pull request to preview how the merged version would work, similar to the idea of Review Apps on Heroku.

Unfortunately, Circle does not support pull requests natively. It can be achieved with a little bit of bash scripting. Let's look at how to set that up.

Go to your GitHub repo and open the `.circleci/config.yml` that we had created above. Replace it with the following:

{% raw %}
``` yaml
version: 2.1

jobs:
  deploy-service:
    docker:
      - image: circleci/node:8.10
    parameters:
      service_path:
        type: string
      stage_name:
        type: string
    steps:
      - checkout

      - run:
          name: Check Pull Request
          command: |
            if [[ ! -z "$CIRCLE_PULL_REQUEST" ]]; then
              # parse pr# from URL https://github.com/fwang/sls-monorepo-with-circleci/pull/1
              PR_NUMBER=${CIRCLE_PULL_REQUEST##*/}
              echo "export PR_NUMBER=$PR_NUMBER" >> $BASH_ENV
              echo "Pull request #$PR_NUMBER"
            fi

      - run:
          name: Merge Pull Request
          command: |
            if [[ ! -z "$PR_NUMBER" ]]; then
              git fetch origin +refs/pull/$PR_NUMBER/merge
              git checkout -qf FETCH_HEAD
            fi

      - restore_cache:
          keys:
            - dependencies-cache-{{ checksum "package-lock.json" }}-{{ checksum "<< parameters.service_path >>/package-lock.json" }}
            - dependencies-cache

      - run:
          name: Install Serverless CLI
          command: sudo npm i -g serverless
            
      - run:
          name: Install dependencies
          command: |
            npm install
            cd << parameters.service_path >>
            npm install

      - run:
          name: Deploy application
          command: |
            cd << parameters.service_path >>
            if [[ ! -z "$PR_NUMBER" ]]; then
              serverless deploy -s pr$PR_NUMBER
            else
              serverless deploy -s << parameters.stage_name >>
            fi

      - save_cache:
          paths:
            - node_modules
            - << parameters.service_path >>/node_modules
          key: dependencies-cache-{{ checksum "package-lock.json" }}-{{ checksum "<< parameters.service_path >>/package-lock.json" }}

workflows:
  build-deploy:
    jobs:
      # non-master branches deploy to stage named by the branch
      - deploy-service:
          name: Deploy Users API
          service_path: services/users-api
          stage_name: ${CIRCLE_BRANCH}
          context: Development
          filters:
            branches:
              ignore: master

      - deploy-service:
          name: Deploy Posts API
          service_path: services/posts-api
          stage_name: ${CIRCLE_BRANCH}
          context: Development
          filters:
            branches:
              ignore: master

      - deploy-service:
          name: Deploy Cron Job
          service_path: services/cron-job
          stage_name: ${CIRCLE_BRANCH}
          context: Development
          filters:
            branches:
              ignore: master

      # master branch deploy to the 'prod' stage
      - deploy-service:
          name: Deploy Users API
          service_path: services/users-api
          stage_name: prod
          context: Production
          filters:
            branches:
              only: master

      - deploy-service:
          name: Deploy Posts API
          service_path: services/posts-api
          stage_name: prod
          context: Production
          filters:
            branches:
              only: master

      - deploy-service:
          name: Deploy Cron Job
          service_path: services/cron-job
          stage_name: prod
          context: Production
          filters:
            branches:
              only: master
```
{% endraw %}

Let's go over the changes we've made.
  - We added a **Check Pull Request** step. We check the built-in environment variable **$CIRCLE_PULL_REQUEST** to decide if the current branch belongs to a pull request. If it does, then we set an environment variable called **$PR_NUMBER** with the pull request id.
  - We also added a **Merge Pull Request** step, where we checkout the merged version of code from GitHub.
  - We then change the **Deploy application** step to deploy to the name the stage **pr#** when deploying a pull request.

Commit these changes to `.circleci/config.yml`.

Next, go to GitHub and create a pull request to the master branch. This will trigger Circle to deployed the merged code with stage name **pr1** to your development account.

### 4. How to clean up unused branches and closed pull requests

After a feature branch is deleted, or a pull request closed, you want to clean up the resources in your AWS account. Circle does not have triggers for these events on GitHub. If you have the credentials for your AWS account, you can perhaps remove the resources by going into each service directory on your local machine and running `serverless remove`. This step is both cumbersome and not ideal.

To get around this limitation, we'll use a little trick. We'll tell Circle to remove a stage (instead of deploying to one) if it sees a Git tag called `rm-stage-STAGE_NAME`.

To do this, go to your GitHub repo and open `.circleci/config.yml` that we created above. Replace it with the following:

{% raw %}
``` yaml
version: 2.1

jobs:
  deploy-service:
    docker:
      - image: circleci/node:8.10
    parameters:
      service_path:
        type: string
      stage_name:
        type: string
    steps:
      - checkout

      - run:
          name: Check Pull Request
          command: |
            if [[ ! -z "$CIRCLE_PULL_REQUEST" ]]; then
              # parse pr# from URL https://github.com/fwang/sls-monorepo-with-circleci/pull/1
              PR_NUMBER=${CIRCLE_PULL_REQUEST##*/}
              echo "export PR_NUMBER=$PR_NUMBER" >> $BASH_ENV
              echo "Pull request #$PR_NUMBER"
            fi

      - run:
          name: Merge Pull Request
          command: |
            if [[ ! -z "$PR_NUMBER" ]]; then
              git fetch origin +refs/pull/$PR_NUMBER/merge
              git checkout -qf FETCH_HEAD
            fi

      - restore_cache:
          keys:
            - dependencies-cache-{{ checksum "package-lock.json" }}-{{ checksum "<< parameters.service_path >>/package-lock.json" }}
            - dependencies-cache

      - run:
          name: Install Serverless CLI
          command: sudo npm i -g serverless
            
      - run:
          name: Install dependencies
          command: |
            npm install
            cd << parameters.service_path >>
            npm install

      - run:
          name: Deploy application
          command: |
            cd << parameters.service_path >>
            if [[ ! -z "$PR_NUMBER" ]]; then
              serverless deploy -s pr$PR_NUMBER
            else
              serverless deploy -s << parameters.stage_name >>
            fi

      - save_cache:
          paths:
            - node_modules
            - << parameters.service_path >>/node_modules
          key: dependencies-cache-{{ checksum "package-lock.json" }}-{{ checksum "<< parameters.service_path >>/package-lock.json" }}

  remove-service:
    docker:
      - image: circleci/node:8.10
    parameters:
      service_path:
        type: string
      stage_name:
        type: string
    steps:
      - checkout

      - restore_cache:
          keys:
            - dependencies-cache-{{ checksum "package-lock.json" }}-{{ checksum "<< parameters.service_path >>/package-lock.json" }}
            - dependencies-cache

      - run:
          name: Install Serverless CLI
          command: sudo npm i -g serverless
            
      - run:
          name: Install dependencies
          command: |
            npm install
            cd << parameters.service_path >>
            npm install

      - run:
          name: Remove application
          command: |
            cd << parameters.service_path >>
            # parse stage name from TAG rm-stage-pr1
            serverless remove -s << parameters.stage_name >>

      - save_cache:
          paths:
            - node_modules
            - << parameters.service_path >>/node_modules
          key: dependencies-cache-{{ checksum "package-lock.json" }}-{{ checksum "<< parameters.service_path >>/package-lock.json" }}

workflows:
  build-deploy:
    jobs:
      # non-master branches deploy to stage named by the branch
      - deploy-service:
          name: Deploy Users API
          service_path: services/users-api
          stage_name: ${CIRCLE_BRANCH}
          context: Development
          filters:
            branches:
              ignore: master

      - deploy-service:
          name: Deploy Posts API
          service_path: services/posts-api
          stage_name: ${CIRCLE_BRANCH}
          context: Development
          filters:
            branches:
              ignore: master

      - deploy-service:
          name: Deploy Cron Job
          service_path: services/cron-job
          stage_name: ${CIRCLE_BRANCH}
          context: Development
          filters:
            branches:
              ignore: master

      # master branch deploy to the 'prod' stage
      - deploy-service:
          name: Deploy Users API
          service_path: services/users-api
          stage_name: prod
          context: Production
          filters:
            branches:
              only: master

      - deploy-service:
          name: Deploy Posts API
          service_path: services/posts-api
          stage_name: prod
          context: Production
          filters:
            branches:
              only: master

      - deploy-service:
          name: Deploy Cron Job
          service_path: services/cron-job
          stage_name: prod
          context: Production
          filters:
            branches:
              only: master

      # remove non-production stages
      - remove-service:
          name: Remove Users API
          service_path: services/users-api
          stage_name: ${CIRCLE_TAG:9}
          context: Development
          filters:
            tags:
              only: /^rm-stage-.*/
            branches:
              ignore: /.*/

      - remove-service:
          name: Remove Posts API
          service_path: services/posts-api
          stage_name: ${CIRCLE_TAG:9}
          context: Development
          filters:
            tags:
              only: /^rm-stage-.*/
            branches:
              ignore: /.*/

      - remove-service:
          name: Remove Cron Job
          service_path: services/cron-job
          stage_name: ${CIRCLE_TAG:9}
          context: Development
          filters:
            tags:
              only: /^rm-stage-.*/
            branches:
              ignore: /.*/
```
{% endraw %}

Let's look at what we changed here:

  - We created a new job called **remove-service**. It's similar to our **deploy-service** job, except it runs `serverless remove`. It assumes the name of the tag is of the format `rm-stage-STAGE_NAME`. It parses for the stage name after the 2nd hyphen.
  - We also set the workflow to run the **remove-service** job for each of our services.

To test this, try tagging the pull request branch before you close the PR.

``` bash
$ git tag rm-stage-pr1
$ git push --tags
```

You'll notice that the **pr1** stage will be removed from your development account.

![View remove services Workflow in CircleCI](/assets/blog/how-to-build-a-cicd-pipeline-for-serverless-apps-with-circleci/view-remove-services-workflow-in-circleci.png)

And that's it! Let's wrap things up next.

#### Next steps

It took us a few steps but we now have a fully-functional CI/CD pipeline for our monorepo Serverless app. It supports a PR based workflow and even cleans up once a PR is merged. The repo used in this guide is available [here with the complete CircleCI configs](https://github.com/seed-run/serverless-example-monorepo-with-circleci).

Some helpful next steps would be to auto-create custom domains for your API endpoints, send out Slack or email notifications, generate CloudFormation change sets and add a manual confirmation step when pushing to production, etc. You also might want to design your workflow to accommodate for any dependencies your services might have. These are cases where the output from one service is used in another. 

Finally, if you are not familiar with Seed, it's worth noting that it'll do all of the above for you out of the box! And you don't need to write up a build spec or do any scripting.
