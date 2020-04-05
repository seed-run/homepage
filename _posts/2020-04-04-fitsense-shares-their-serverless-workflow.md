---
layout: post
title: FitSense shares their Serverless workflow
categories: community
author: stephie
---

[FitSense](https://www.fitsense.io) recently shared a blog post detailing their Serverless development workflow. They use Serverless, AWS CloudFormation, and Seed to automatically bring up and tear down new environments.

![FitSense landing page](/assets/blog/fitsense-shares-their-serverless-workflow/fitsense-landing-page.png)

[Mitchell Shelton](https://www.linkedin.com/in/mitchell-shelton/) from the [FitSense](https://www.fitsense.io) team [recently wrote about the key lessons they learnt from scaling their development environment](https://medium.com/@mitchellshelton97/key-lessons-learnt-from-scaling-a-development-environment-2c1af911c31). They used [Seed]({{ site.url }}) to allow their developers to automatically create their own completely isolated environments.

To create a new Serverless environment, the developers on the FitSense team simply need to:

``` bash
$ git checkout -b popup-stack
$ git push origin popup-stack
```

And to tear it down:

``` bash
$ git push -d origin popup-stack
```

We've written about [git workflow for Serverless apps]({% link _posts/2019-07-26-git-workflow-for-serverless-apps.md %}) on our blog before. But it's really great to see teams share their experiences with implementing these workflows. You get a firsthand account of the motivations and challenges involved.

So make sure to [check out their blog post](https://medium.com/@mitchellshelton97/key-lessons-learnt-from-scaling-a-development-environment-2c1af911c31)! And [let us know](mailto:{{ site.email }}) how your team is using Seed to improve your Serverless development workflow!
