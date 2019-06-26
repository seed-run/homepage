---
layout: build-errors
title: Common Serverless Errors
description: Common Serverless Errors is a collection of the most common Serverless Framework errors developers run into on AWS. Also listed, is an explanation of why the error occurred and what you can do to fix it.
image: /assets/social-cards/common-errors.png
---

Common Serverless Errors is a compilation of some of the most common Serverless Framework AWS errors and how to fix them. Available as [an open source GitHub repo]({{ site.github_repo }}{{ site.github_repo_errors_path }}), edits and contributions are welcome!

<div class="build-error-header-controls">
  <div class="panel">
    <a href="mailto:?&cc=&bcc=&subject=Debug Serverless Errors&body=Check out this great resource for debugging Serverless errors on AWS - https://seed.run/docs/serverless-errors/">
      <i class="fa fa-envelope" aria-hidden="true"></i>
    </a>
    <a target="_blank" href="https://twitter.com/intent/tweet?url=https%3A%2F%2Fseed.run%2Fdocs%2Fserverless-errors%2F&via=SEED_run&text=Check%20out%20this%20great%20resource%20for%20debugging%20Serverless%20errors%20on%20AWS">
      <i class="fa fa-twitter" aria-hidden="true"></i>
      <span>Share</span>
    </a>
  </div>
  <div class="panel">
    <a href="javascript:alert('Please bookmark this page in your browser')">
      <i class="fa fa-bookmark" aria-hidden="true"></i>
      <span>Bookmark</span>
    </a>
  </div>
  <div class="panel">
    <a target="_blank" href="{{ site.github_repo }}/issues/new?assignees=jayair&labels=enhancement&template=common-serverless-errors.md&title=%5BSLS+ERR%5D">
      <i class="fa fa-plus-square" aria-hidden="true"></i>
      <span>Contribute</span>
    </a>
  </div>
</div>

<ul class="build-error-list fa-ul">
  {% for item in site.data.build-errors.toc %}
    <li>
      <i class="fa-li fa fa-file-text-o"></i>
      <a href="{{ item.url }}">{{ item.title }}</a>
    </li>
  {% endfor %}
</ul>

---

#### About

While working on your Serverless app on AWS, you might notice that some of the errors can be really hard to debug. It can either be an obscure AWS error or it might just have a misleading error message.

At [Seed](/), we've had a chance to help a lot of our users work through some of these issues. We decided to catalogue the errors and their fixes. We think this will be useful for future reference and something the Serverless community can use.
