---
layout: page
title: Scratchpad
permalink: /scratchpad/
---

Normally I keep all my locally, using
[vimwiki](https://github.com/vimwiki/vimwiki/). These include code snippets,
shortcuts, hints, cheatsheets to programs, command line tools to try, or really
random thoughts of mine with regards to a specific technical subject. But since
I struggle to post new articles on a consistent basis I decided to put some more
structure into a few of these notes and post them instead. These would by no
means constitute fully-fledged well-written articles (the very opposite!).  But
I hope they may help someone that ends up having the same issue I eventually
solved.

<div class="scratchpad_posts">
  <ul class="post-list">
    {% assign posts = site.tags["scratchpad"] %}
    {% for post in posts %}
    <li>
      <span class="post-meta">{{ post.date | date: "%b %-d, %Y" }}</span>
      <h2>
        <a class="post-link" href="{{ post.url | relative_url }}">{{ post.title | escape }}</a>
      </h2>
    </li>
    {% endfor %}
  </ul>

  <p class="rss-subscribe">subscribe <a href="{{ "/feed.xml" | relative_url }}">via RSS</a></p>

</div>
