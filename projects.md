---
layout: page
title: Projects
permalink: /projects.html
---

Below is a complete index of the analytical models, data frameworks, and technical case studies I have built. Click any project title to read the full end-to-end breakdown.

<ul class="post-list" style="list-style: none; padding: 0; margin-top: 30px;">
  {% for post in site.posts %}
    <li style="margin-bottom: 45px; border-bottom: 1px dashed rgba(0,0,0,0.15); padding-bottom: 25px;">
      <span class="post-meta" style="font-size: 0.95rem; color: #666; display: block; margin-bottom: 8px; font-family: sans-serif;">
        {{ post.date | date: "%B %d, %Y" }}
      </span>
      <h2 style="margin: 0 0 12px 0; font-size: 1.75rem;">
        <a href="{{ post.url | relative_url }}" style="color: #000; text-decoration: none; font-weight: bold; border-bottom: none;">
          {{ post.title }}
        </a>
      </h2>
      {% if post.excerpt %}
        <p style="margin: 0; color: #333; line-height: 1.7; font-size: 1.1rem; font-family: serif;">
          {{ post.excerpt | strip_html | truncatewords: 35 }}
        </p>
      {% endif %}
    </li>
  {% endfor %}
</ul>
