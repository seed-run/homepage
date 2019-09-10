---
layout: post
title: How to improve AWS Lambda Cold Start performance
categories: community
author: erez
excerpt: One of the great promises of serverless has always been that it would free developers to focus on writing code without having to give too much consideration to the underlying infrastructure.
canonical_url: https://lumigo.io/blog/how-to-improve-aws-lambda-cold-start-performance/
---

_The article, [How to Improve Lambda Cold Start Performance](https://lumigo.io/blog/how-to-improve-aws-lambda-cold-start-performance/?utm_source=seed&utm_medium=crosspost), was first published on the Lumigo blog._

_Discover how your team can slash the time it spends monitoring & troubleshooting AWS serverless apps with [Lumigo](https://lumigo.io/product/)._

---

One of the great promises of serverless has always been that it would free developers to focus on writing code without having to give too much consideration to the underlying infrastructure. But the advantages presented by the instantly, infinitely scalable nature of serverless come with limitations and unique considerations that you need to take into account.

Among the biggest issues we - a 100% serverless company - have faced, are [cold starts](https://lumigo.io/learn/what-causes-an-aws-lambda-cold-start/), the extra time it takes for a function to execute when it hasn’t recently been invoked.  

Cold starts can be a killer, especially if you’re developing a customer-facing application that needs to operate in real time. They happen because if your lambda is not already running, AWS needs to deploy your code and spin up a new container before the request can begin. This can mean a request takes much longer to execute, and only when the container is ready can your lambda start running.

### Cold starts are a necessary evil

The fact of the matter is that cold starts are a necessary byproduct of the scalability of serverless. 

AWS needs a ready supply of containers to spin up when functions are invoked. That means that functions are kept warm for a limited amount of time (usually **30 - 45 minutes**) after executing, before being spun down so that container is ready for any new function to be invoked.

![Function lifecycle](/assets/blog/how-to-improve-aws-lambda-cold-start-performance/function-lifecycle.png)
*Source: [Become a Serverless Black Belt - Optimizing Your Serverless Applications - AWS Online Tech Talks](https://www.slideshare.net/AmazonWebServices/become-a-serverless-black-belt-optimizing-your-serverless-applications-aws-online-tech-talks/14)*

Cold starts account for less than **0.25%** of requests but the impact can be huge, sometimes requiring [**5 seconds**](https://mikhail.io/serverless/coldstarts/aws/) to execute the code. This issue is particularly relevant to applications that need to run executions in real-time, or those that rely on split-second timing.

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Interesting - cold starts affect less than 0.25% of all Lambda invocations. <a href="https://twitter.com/hashtag/ServerlessConf?src=hash&amp;ref_src=twsrc%5Etfw">#ServerlessConf</a> <a href="https://twitter.com/chrismunns?ref_src=twsrc%5Etfw">@chrismunns</a></p>&mdash; James Beswick @ Seattle (@jbesw) <a href="https://twitter.com/jbesw/status/917850944888598528?ref_src=twsrc%5Etfw">October 10, 2017</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

It’s widely known that AWS has been working consistently to “solve” the cold start issue once and for all, and while improvements have been incremental, a plan to improve the startup performance of Lambdas inside VPCs was announced at re:Invent 2018.

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Looks like <a href="https://twitter.com/awscloud?ref_src=twsrc%5Etfw">@awscloud</a> has some ideas to fix <a href="https://twitter.com/hashtag/Lambda?src=hash&amp;ref_src=twsrc%5Etfw">#Lambda</a> cold starts in a <a href="https://twitter.com/hashtag/VPC?src=hash&amp;ref_src=twsrc%5Etfw">#VPC</a>. 🙌 Coming in 2019! <a href="https://twitter.com/hashtag/serverless?src=hash&amp;ref_src=twsrc%5Etfw">#serverless</a> <a href="https://twitter.com/hashtag/reInvent?src=hash&amp;ref_src=twsrc%5Etfw">#reInvent</a> <a href="https://t.co/9wPys1Jf6x">pic.twitter.com/9wPys1Jf6x</a></p>&mdash; Jeremy Daly (@jeremy_daly) <a href="https://twitter.com/jeremy_daly/status/1068272580556087296?ref_src=twsrc%5Etfw">November 29, 2018</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

### 5 ways to improve cold start performance

While cold start times are a real issue, the good news is that there are very useful tools and approaches that can help to mitigate the problem, either by avoiding cold starts altogether or reducing their duration.

#### Monitor

Monitoring can be a challenge in a serverless environment, but it’s a critical first step to being able to address areas of inefficiency in your application.

Both CloudWatch Logs and X-Ray can help you to identify where and when cold starts are occuring in your application, although it requires some active process of deduction on your part. Monitoring will also help you identify which cold starts are truly problematic to the smooth running of your application and satisfaction of users, and which can be safely ignored.

There are also several commercial tools, our platform [**Lumigo**](https://www.lumigo.io/) among them, that make it much easier to monitor whether - and how often - your application is being affected by cold starts.

#### Keep lambdas warm

As we noted above, Lambdas are kept warm by AWS for a limited time after being invoked, “[in anticipation of another Lambda function invocation](https://docs.aws.amazon.com/lambda/latest/dg/running-lambda-code.html)”. Warm Lambdas will always give you faster execution times.

One thing you can do to guard against cold starts is to ensure that your Lambdas do not become inactive. Tools such as the [**Lambda Warmer**](https://www.npmjs.com/package/lambda-warmer) by [Jeremy Daly](https://twitter.com/jeremy_daly) or the [**Serverless Plugin Warmup**](https://github.com/FidelLimited/serverless-plugin-warmup), created by the team at [Fidel](https://twitter.com/FidelHQ), invoke the lambdas at a given interval to ensure that the containers aren’t destroyed.

#### Reduce the number of packages

We’ve seen that the biggest impact on AWS Lambda cold start times is not the size of the package but the initialization time when the package is actually loaded for the first time.

The more packages you use, the longer it will take for the container to load them. Tools such as [**Browserify**](http://browserify.org/) and [**Serverless Plugin Optimize**](https://www.npmjs.com/package/serverless-plugin-optimize) can help you reduce the number of packages.

**Related Research** - [**Web Frameworks Implication on Serverless Cold Start Performance in NodeJS**](https://lumigo.io/blog/web-frameworks-implication-on-serverless-cold-start-performance-in-nodejs/)

#### Choose the right language

There is no doubt that your choice of programming language will have an effect on the length of the cold start times you see. 

In [one experiment](https://medium.com/@nathan.malishev/lambda-cold-starts-language-comparison-%EF%B8%8F-a4f4b5f16a62), Nathan Malishev found that **Python**, **Node.js** and **Go** took much less time to initialize than **Java** or **.NET**, with Python performing at least twice as quickly compared to Java, depending on memory allocation.

![Cold Start languages performance](/assets/blog/how-to-improve-aws-lambda-cold-start-performance/cold-start-languages-performance.png)
*Source: [Lambda Cold Starts, A Language Comparison - Nathan Malishev](https://medium.com/@nathan.malishev/lambda-cold-starts-language-comparison-%EF%B8%8F-a4f4b5f16a62)*

#### Get Lambdas out of VPC

Unless it’s really necessary (for instance, to access resources within a VPC) try to get your Lambdas running outside of your VPC, as the attachment of the ENI interfaces can have [a huge impact on cold start times](https://medium.freecodecamp.org/lambda-vpc-cold-starts-a-latency-killer-5408323278dd).

In [these experiments](https://www.simplybusiness.co.uk/about-us/tech/2019/03/aws-lambda-cold-start-vpc/) run by Alessandro Morandi, he found that a Lambda with 3GB of memory took up to 30x longer to invoke from a cold start when inside a VPC compared to outside a VPC.

And as Yan Cui pointed out [in a recent article](https://lumigo.io/blog/to-vpc-or-not-to-vpc-in-aws-lambda/), while VPCs provide necessary protection to EC2s, they aren’t required to provide that kind of security to Lambdas. 

![AWS VPC decision tree](/assets/blog/how-to-improve-aws-lambda-cold-start-performance/aws-vpc-decision-tree.png)
*Source: [Serverless Applications Lens - AWS Well-Architected Framework](https://d1.awsstatic.com/whitepapers/architecture/AWS-Serverless-Applications-Lens.pdf)*

**Update**

Following the recent [announcement by AWS](https://aws.amazon.com/blogs/compute/announcing-improved-vpc-networking-for-aws-lambda-functions/) (September 2019), it seems that performance issues affecting Lambdas inside VPCs could soon be a thing of the past.
Leveraging **Hyperplane**, the Network Function Virtualization platform, AWS is claiming “dramatic improvements to [Lambda] function startup performance” inside VPCs. It all looks very promising, but we’ll wait until the update is fully rolled out over the next couple months before changing our recommendations.

### Conclusion

As we’ve seen, there are a variety of ways to reduce the impact of cold starts, but unfortunately none of them can be relied upon to completely solve the problem in every situation. 

The best advice is to monitor your application and focus most effort only on the cold starts that have a direct effect on user experience or the smooth running of your application.

Lambda cold start times have become something of an obsession of the first wave of serverless adopters, and that’s not likely to change anytime soon. It’s one of the few niggles affecting a really exciting new way to build software.

But there’s little doubt that Amazon (and the other cloud platform providers) will continue to work away on this problem until it’s no longer an issue. And when they do, you can be sure that we will be raising a frosty beer in their honor!
