# Should I Use Hosted Or On-Premise CI

We are going to take a look at hosted versus on-premise CI solutions. You can weigh the pros and cons and decide what's best for your team.

## Quick to start

There is a learning curve when using a hosted CI service. Most of the time spent setting up your pipeline using a hosted service is to learn how the service works. The learning curve can drastically vary from a service like Seed on the simple side, to Jenkins on the complicated side. If you pick a service like Seed, Travis CI, CircleCI, this time is usually much shorter than setting up your own pipeline from scratch.

## Cost

For on-prem CI, the cost for your pipeline is simply your infrastructure cost. If you are on AWS, this is the EC2 cost to run your build machine. You can take advantage of the EC2 free tier to get started for free.

Most CI service provides a generous free tier for you to get started for free as well. Seed is free for the first 500 minutes, which is more than enough for deploying 10 times a day for a simple project.

When you factor in the devops cost for setting up the pipeline and maintaning it, on-prem CI is very expensive to get started. And the responsibility of keeping the pipeline maintained usually falls on the CTO or tech lead in a small to medium sized team, which is not a good spend of their time.

## **Flexible Infrastructure**

For on-prem CI, you have the complete control over the underlying infrastructure. You can spin up your build machine with any vCPU, RAM and disk space. On the other hand, CircleCI supports up to 16GB RAM and 8vCPU; and CodeBuild supports up to 15GB RAM and 8vCPU.

This is usually not a concern when getting started, as 16GB and 8vCPU is more than enough for most projects.

## **Customizable**

With on-prem CI, you can create something to fit your exact pipeline need. As your pipeline grows more complicated, you don't have to won't you grow the feature-set offered by a CI service.

That being said, common features like:

- git push to deploy
- deploying pull requests
- slack notification and workflow integrations

are now provided out of the box for most hosted CI services. The feature-set they offer goes to a great extend.

## **Security**

For on-prem CI, because the pipeline lives and run within your own infrastructure, you can easily secure and comply with company's security policy. This is requires some integration when dealing with a hosted CI service.

With hosted CI, you have to wait to hear from your service provider when there's an outage, maintenance, or any other form of downtime. But bare in mind, unless you have a dedicated devops person/team to manage your pipeline, you might not be able to provide a better uptime hosting yourself.

Also, a hosted CI service usually charge a lot more when you talk security and compliances with them.

## Conclusion

The key decision is do you have a devops person/team to manage your pipeline. If you are a small to medium sized team, definitely use a hosted CI service. The setup process is usually very quick, in fact it takes most teams less than 15 minutes to setup their pipeline and make their first deployment on Seed. There is minimal maintanence and you can get started for free.

On the other hand, if you have specific requirements about your pipeline, either that's the infrastructure requirements or security compliance, go with on-prem. It gives you full control over your pipeline.
