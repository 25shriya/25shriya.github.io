---
layout: page
title: Health and Disability
---

<p>
    I was diagnosed with Type 1 diabetes at the age of 18. This has led me to explore various aspects of nutrition, fitness regimes and new tech for diabetics since. I continue to understand what fits best for me in terms of holisting living. Stay tuned for more updates on my journey!
    <br><br>
    DISCLAIMER: The content shared here is based solely on personal experiences and anecdotes. It is NOT medical advice and SHOULD NOT be taken as such. Always seek the guidance of a qualified healthcare professional regarding your concerns.
</p>


<ul>
  {% for post in site.posts %}
    {% if post.path contains '_posts/diabetes/' %}
      <li>
        <a href="{{ post.url}}">{{ post.title }}</a>
      </li>
    {% endif %}
  {% endfor %}
</ul>