---
layout: post
title: Blog
---

<ul class="post-list">
  {% for post in site.posts %}
    <li>
      <h3>
        <a
          href="https://www.linkedin.com/in/{{ site.data.authors[post.author].linkedin }}/"
        >
          <img
            width="36"
            class="bullet"
            title="{{ site.data.authors[post.author].name }}"
            src="{{ site.data.authors[post.author].picture }}"
          />
        </a>
        <a href="{{ post.url }}">{{ post.title }}</a>
      </h3>
      <div>{{ post.excerpt }}</div>
      <div class="post-info">
        <a href="{{ post.url }}">
          View post
        </a>
        <span class="separator">&nbsp;&bull;&nbsp;</span>
        <span class="date">{{ post.date | date: '%B %d, %Y' }}</span>
      </div>
    </li>
  {% endfor %}
</ul>
