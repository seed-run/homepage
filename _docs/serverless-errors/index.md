---
layout: docs
title: Common Serverless Errors
image: /assets/social-cards/common-errors.png
---

While working on your [Serverless](https://serverless.com) app on AWS, you might notice that some of the errors can be really hard to debug. It can either be an obscure AWS error or it might just have a misleading error message.

At [Seed](/), we've had a chance to help a lot of our users work through some of these issues. We decided to catalogue the errors and their fixes. We think this will be useful for both future reference and something the Serverless community can use.

<ul class="build-errors-list fa-ul">
  {% for item in site.data.build-errors.toc %}
    <li>
      <i class="fa-li fa fa-file-text-o"></i>
      <a href="{{ item.url }}">{{ item.title }}</a>
    </li>
  {% endfor %}
</ul>
