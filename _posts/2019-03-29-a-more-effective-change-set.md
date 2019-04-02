---
layout: post
title: A More Effective Change Set
author: frank
---

Over the last few weeks we've made several changes to the way we handle build artifacts. These have allowed us to rollout an update to make the promote change set in Seed far more useful and effective.

![Seed promote change set](/assets/blog/a-more-effective-change-set/seed-promote-change-set.png)

Before we get into the details of the update, let's quickly look at the problems with change sets.

![Old Change Set](/assets/blog/a-more-effective-change-set/old-change-set.png)

- Poorly categorized changes

  The biggest problem was that all the changes generated as a part of a CloudFormation Change Set were displayed together. Any sufficiently complicated commit generates dozens of CloudFormation changes. And while some of these changes were useful, most of them were a part of routine updates.

- Not humanly readable

  The changes were also in the standard CloudFormation format, making them very hard to read. It also wasn't clear which resource was being changed. Since all that was visible were the resource ids.

To fix these we decided to generate the change set ourself, instead of relying on CloudFormation Change Sets. Here are some of the key things we do with the new change sets.

We automatically figure out if a change is import and mark it as "major" (or "minor"). We collapse the minor ones, so it's pretty clear that you only need to review the major changes.

![Major Change Set](/assets/blog/a-more-effective-change-set/major-change-set.png)

We also don't bug you to review the changes if there are no major changes.

![No major changes Change Set](/assets/blog/a-more-effective-change-set/no-major-changes-change-set.png)

But you can always click to see the minor changes.

![View minor changes Change Set](/assets/blog/a-more-effective-change-set/view-minor-changes-change-set.png)

Finally, you can send us a quick report if you think we've miscategorized some of the changes.

![Report Change Set](/assets/blog/a-more-effective-change-set/report-change-set.png)

A more effective way to review your infrastructure changes before promoting them is just one way Seed is helping you manage deployments for your Serverless Framework application.
