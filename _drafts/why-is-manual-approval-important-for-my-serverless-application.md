Why is manual approval important for my Serverless application?

### Deploying Code

In a traditional monolithic application development, your code mostly contains application logic. Application logic can be rolled back relatively easily and side-effect free.

### Deploying Database Migrations

The deployment process gets tricky when you have database migration scripts that get executed automatically. When you do that, having migration rollbacks scripts in place in the case of rollback is always tricky. Up till this point, your code change and infrastructure change are fairly separate.

### Deploying Infrastructure

Serverless application adopts the infrastructure as code pattern, and your infrastructure definition (serverless.yml) sits in your codebase. When your serverless app is deployed, code is updated and the infrastructure changes are applied.

A typo in serverless.yml could remove your resources. And in the case of a database resource, this could result in permanent data loss. There are multiple way to prevent such data loss - read here to learn [how to prevent accidentally deleting Serverless resources]([https://seed.run/blog/how-to-prevent-accidentally-deleting-serverless-resources](https://seed.run/blog/how-to-prevent-accidentally-deleting-serverless-resources))

### Infrastructure Diffs

But you want to prevent such errors in the first place. Just like you often do code review, an infrastructure review is also important, if not more important. Luckily CloudFormation provides a feature called Changeset. You give CloudFormation the new template you are going to deploy into a stack, and CloudFormation will show you the resources that are going to be added, modified and removed. You can think of it as a dry run.

CloudFormation Changeset has a down side, it is very hard to read. Here is why. Serverless Framework does a really good job of allowing to provision a Lambda and API resources in a simple and compact syntax. Behind the scene, a great number of resources are provisioned: Lambda roles, Lambda versions, Lambda log groups, API Gateway resource, API Gateway method, API Gateway deployment, just to name a few. When CF shows you a list of changes with these resource, usually with cryptic names, it requires a great extend of CF knowledges to understand the changes.

That's why on Seed we take the Change Set to the next level by showing changes that are relavent to the developer and highlighting the changes that should be paid extra attention to. By reviewing the Change Set before promoting to production, we think this extra step can really help prevent any irreversible infrastructure changes from being deployed to your production environment mistakingly.

You can learn more about it here - [https://seed.run/docs/promoting-to-production](https://seed.run/docs/promoting-to-production)
