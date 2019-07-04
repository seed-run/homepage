# How to build a CI/CD pipeline for monorepo Serverless apps with CircleCI?

A monorepo Serverless app is a git repo with multiple Serverless services each sitting in a subfolder with its own serverless.yml file. Here is a [template repo](https://github.com/fwang/sls-monorepo-with-circleci). Code structure looks like:

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

### We will be covering:
- How to deploy your monorepo app on git push
- How to deploy to multiple AWS accounts
- How to deploy in pull request workflow
- How to clean up unused branches and closed pull requests

### Pre-requisites
- A [CircleCI account](https://circleci.com)
- AWS credentials (Access Key Id and Secret Access Key) of the AWS account you are going to deploy to. Follow (this guide)[https://serverless-stack.com/chapters/create-an-iam-user.html] to create one.
- Go to the [template repo](https://github.com/seed-run/serverless-template-monorepo) and click on **Use this template** to clone the template
![](https://i.imgur.com/CwYX6nT.png)

### How to deploy your monorepo app on git push

- Go into your [CircleCI account](https://circleci.com)
- Select **Contexts** from the left menu, and click **Create Context**
![](https://i.imgur.com/u2eQtbC.png)

- Create a context called **Development**
![](https://i.imgur.com/qOvn1lg.png)

- Go in to the **Development** context, and click on **Add Environment Variable**
![](https://i.imgur.com/j5iEfua.png)

- Create an variable with
  - Name: **AWS_ACCESS_KEY_ID**
  - Value: Access Key Id of the IAM user
![](https://i.imgur.com/BVAwoY4.png)

- Repeat the step and create another variable with
  - Name: **AWS_SECRET_ACCESS_KEY**
  - Value: Secret Access Key of the IAM user

![](https://i.imgur.com/kFJ0qgC.png)


- Go to the cloned repository and click on **Create new file**
![](https://i.imgur.com/I6OPCr0.png)

- Name the new file **.circleci/config.yml** and paste the following content

```yaml=
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
            sls deploy -s << parameters.stage_name >>

      - save_cache:
          paths:
            - node_modules
            - services/users-api/node_modules
          key: dependencies-cache-{{ checksum "package-lock.json" }}-{{ checksum "<< parameters.service_path >>/package-lock.json" }}

workflows:
  build-deploy:
    jobs:
      - deploy-service:
          service_path: services/users-api
          stage_name: ${CIRCLE_BRANCH}
          context: Development
      - deploy-service:
          service_path: services/posts-api
          stage_name: ${CIRCLE_BRANCH}
          context: Development
      - deploy-service:
          service_path: services/cron-job
          stage_name: ${CIRCLE_BRANCH}
          context: Development
```

- A couple of things to note:
  - We created a job called **deploy-service**, that takes the **path of a service** and the **name of the stage** you want to deploy to, which will be used for `--stage` in Serverless commands.
  - The **deploy-service** job does a `npm install`  repo's root directory and again in the service directory
  - The job then goes into the service directory and runs `sls deploy` with the stage name that's passed in
  - We also created a workflow that run the **deploy-service** job for each service, and passing in the branch name as the stage name.
  - As a side note, we also specified that we want to cache the **node_modules** folder in both the root direrctory and the service directory for faster deployment.


- Scroll to the bottom and click **Commit new file**
- Select **ADD PROJECTS** on the left menu, and click on the 'Set Up Project' button next to your project. Make sure the 'Show forks' checkbox is checked.
![](https://i.imgur.com/dy3UqvQ.png)

- Select 'Linux' as the Operating System, and 'Node' as the Language.
- Go to step 5 and click on 'Start building'.
- Go to your CircleCI console and clicks on **WORKFLOWS** on the left menu
![](https://i.imgur.com/J3icQIH.png)
- Click on the workflow, you will see the 3 jobs that are currently running or have finished running.
![](https://i.imgur.com/XWqrgd4.png)
- Click on a job, you will see the output for each step. Scroll down to the **Deploy application** section, and you should see the output for `sls deploy -s master`
![](https://i.imgur.com/8lJYVat.png)


### How to deploy to multiple AWS accounts

```yaml=
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
              sls deploy -s pr$PR_NUMBER
            else
              sls deploy -s << parameters.stage_name >>
            fi

      - save_cache:
          paths:
            - node_modules
            - services/users-api/node_modules
          key: dependencies-cache-{{ checksum "package-lock.json" }}-{{ checksum "<< parameters.service_path >>/package-lock.json" }}

workflows:
  build-deploy:
    jobs:
      # non-master branches deploy to stage named by the branch
      - deploy-service:
          service_path: services/users-api
          stage_name: ${CIRCLE_BRANCH}
          context: Development
          filters:
            branches:
              ignore: master
      - deploy-service:
          service_path: services/posts-api
          stage_name: ${CIRCLE_BRANCH}
          context: Development
          filters:
            branches:
              ignore: master
      - deploy-service:
          service_path: services/cron-job
          stage_name: ${CIRCLE_BRANCH}
          context: Development
          filters:
            branches:
              ignore: master

      # master branch deploy to the 'prod' stage
      - deploy-service:
          service_path: services/users-api
          stage_name: prod
          context: Production
          filters:
            branches:
              only: master
      - deploy-service:
          service_path: services/posts-api
          stage_name: prod
          context: Production
          filters:
            branches:
              only: master
      - deploy-service:
          service_path: services/cron-job
          stage_name: prod
          context: Production
          filters:
            branches:
              only: master
```

![](https://i.imgur.com/HuxeLAN.png)
