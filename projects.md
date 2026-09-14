---
layout: home
title: Projects
permalink: /projects/
---

<!-- 🛠️ THIN CONTAINER TO PREVENT NARROW SQUEEZING ON LAPTOPS -->
<div style="width: 100%; max-width: 820px; margin: 0 auto 40px auto; padding: 0 20px; box-sizing: border-box; display: block;">
  <h1 class="content-title divided" style="margin-bottom: 20px; font-size: 2rem; font-weight: bold; text-align: center;">Master Project Index</h1>
  
  <p style="font-size: 1.2rem; line-height: 1.7; color: #111; text-align: center; margin-bottom: 40px; font-family: serif;">
    Below is a complete index of the analytical models, data frameworks, and technical case studies I have built. Click any project title to read the full end-to-end breakdown, including data modeling workflows, SQL source scripts, and interactive dashboard links.
  </p>
</div>

<!-- 🛠️ CUSTOM MASTER LOOP LISTING ALL PROJECTS WITHOUT 3-PAGE LIMITS -->
<div style="width: 100%; max-width: 820px; margin: 0 auto; padding: 0 20px; box-sizing: border-box;">
  <ul class="post-list" style="list-style: none; padding: 0; margin: 0;">
    {% for post in site.posts %}
      <li style="margin-bottom: 40px; border-bottom: 1px dashed rgba(0,0,0,0.15); padding-bottom: 25px;">
        <span class="post-meta" style="font-size: 0.95rem; color: #333; display: block; margin-bottom: 8px; font-family: sans-serif;">
          {{ post.date | date: "%B %d, %Y" }}
        </span>
        <h2 style="margin: 0 0 12px 0; font-size: 1.75rem;">
          <a href="{{ post.url | relative_url }}" style="color: #000; text-decoration: none; font-weight: bold; border-bottom: 2px solid #000;">
            {{ post.title }}
          </a>
        </h2>
        {% if post.excerpt %}
          <p style="margin: 0; color: #111; line-height: 1.7; font-size: 1.1rem; font-family: serif;">
            {{ post.excerpt | strip_html | truncatewords: 35 }}
          </p>
        {% endif %}
      </li>
    {% endfor %}
  </ul>
</div>