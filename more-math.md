---
layout: page
title: More Math!
---

<ul>
  {% for post in site.posts/math %}
    {% if post.path contains '_posts/math/' %}
      <li>
        <a href="{{ post.url}}">{{ post.title }}</a>
      </li>
    {% endif %}
  {% endfor %}
  <li><a href="https://drive.google.com/file/d/1jlY4ZPVFVQ_nPcgFVmuI1YQSW2HWSynr/view?usp=sharing">Here's</a> a list of ideas and open problems in commutative algebra and number theory compiled by me.</li>
</ul>

