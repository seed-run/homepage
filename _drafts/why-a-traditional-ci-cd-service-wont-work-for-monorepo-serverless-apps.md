# Why a traditional CI/CD service won't work for monorepo Serverless apps?

Let's first look how a monorepo Serverless app is different from a traditional monolithic app:

- App structure: a monorepo app is made  up of a collection of services. These services are loosely coupled, independently testable and independently deployable.
- Tests: each service comes with it own unit tests that are side-effect free from other services. The tests can be run independently.
- Deployments: each service can be deployed independently. And not all services need to be deployed on each git push. Only changed services need to be deployed.

Now let's see how this architecture shift changes our CI/CD pipeline.

A bit of background. Tradition CI/CD services give you a build instance that's available to you 24/7 to run your pipeline. Think of it like an EC2 instance with the pipeline application preloaded on it. On git push, your build instance pulls the code from git, run some tests, packages your code and deploys it. This works great for monolithic app since you are testing your application as a whole and deploys it as a whole.

With Serverless apps, you test and deploy each service independently, and you want to do them concurrently to speed up the build/test process. This poses a problem. If you have to 2 services, and you want to deploy them concurrently, you would need to pay for 2 build servers, and the cost scales with the number of services you want to deploy concurrently. This means you either deploy your services sequentially and have a slow pipeline; or deploy them all in parallel and have an expensive pipeline.

Ideally you want to use a micro-service friendly CI/CD service that facilitates bursts of highly concurrent deployments. Seed and AWS CodeBuild are two services of such. Your cost scales with the amount of build minutes you use, and you essentially have unlimited concurrency.
