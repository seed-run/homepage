# Why is rollback strategy different for Serverless apps?

### A brief background on Deployment Artifacts

When building traditional applications like an Express or Rails app, you have the concept of **Immutable Artifacts**. You package the code you want to deploy and label it with a unique build id. This package then gets deployed to different environments for various integration/uat/end-to-end tests, before it gets finally deployed into the Production environment. Throughout the journey of traveling downstream, your code is only packaged once in the beginning when the  artifact is created, hence the **Immutable** part.

### Rollback for traditional applications

What does this mean in the context of a NodeJS app? When you package the code, you run npm install to pull in your dependencies; you might run eslint to apply fixes; you might run webpack to transpile your code; in the end it you end up with a deployment artifact, usually a .zip file. When you need to deploy it to a given environment, you simply upload and unzip the artifact on the NodeJS server. The deployment process is extremely simple.

When you need to rollback, you simply fetch the .zip artifact file from a previous build, upload and unzip. This is the preferred rollback strategy over the re-deploying an older version of code. 

### Rollback for Serverless applications

Unfortunately, deployment artifact isn't everything that goes into a build for Serverless applications. A bit of background. Serverless Framework created a really collaborative community by allowing people create plugins to simplify the development process. Plugins can inject custom actions during various Serverless lifecycle. For example, the popular serverless-webpack plugin transpiles your code during the 'serverless package' process; while another popular serverless-domain-manager plugin sets up your API custom domain during the 'serverless deploy' process.

This is problematic from the **Immutable** perspective in two ways. Here is why:

1. Plugins that inject into the deployment process can result in side-effect changes.
2. Serverless Framework require all plugins be installed during deployment (ie. serverless deploy). Hence, even with the deployment artifact in hand (link to post on how to create deployment artifact for Serverless), you still need to obtain the source code along with all plugin dependencies installed in order to deploy. 

### How should I rollback?

The best way to rollback can be considered as a re-deploy with previously package artifact from `serverless package`. You don't rebuild the code, but the plugins will do a re-deploy.
