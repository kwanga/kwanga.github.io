---
layout: default
title: Projects
permalink: /projects.html
---

<div style="background-color: #f2c811; min-height: 100vh; width: 100%; display: block; margin: 0; padding: 20px 0; box-sizing: border-box; clear: both;">
  
  <!-- CONTAINER TO FORWARD HEADER AND BODY ELEMENTS TOGETHER -->
  <div style="max-width: 800px; margin: 0 auto; padding: 0 20px; box-sizing: border-box;">
    
    <!-- HEADER MARGIN PADDING EXTRA SPACE -->
    <div style="text-align: center; margin-bottom: 40px; margin-top: 20px;">
      <h1 style="font-size: 2.2rem; font-weight: bold; color: #000; margin-bottom: 15px; font-family: serif; border: none;">Master Project Index</h1>
      <p style="font-size: 1.2rem; line-height: 1.7; color: #111; font-family: serif; max-width: 680px; margin: 0 auto;">
        Below is a complete index of the analytical models, data frameworks, and technical case studies I have built. Click any project title to read the full end-to-end breakdown.
      </p>
    </div>

    <!-- DYNAMIC TIMELINE POST LIST LOOP -->
    <ul class="post-list" style="list-style: none; padding: 0; margin: 0;">
      {% for post in site.posts %}
        <li style="margin-bottom: 45px; border-bottom: 1px dashed rgba(0,0,0,0.2); padding-bottom: 25px;">
          <span class="post-meta" style="font-size: 0.95rem; color: #222; display: block; margin-bottom: 8px; font-family: sans-serif; font-weight: 500;">
            {{ post.date | date: "%B %d, %Y" }}
          </span>
          <h2 style="margin: 0 0 12px 0; font-size: 1.8rem;">
            <a href="{{ post.url | relative_url }}" style="color: #000; text-decoration: none; font-weight: bold; border-bottom: 2px solid #000; padding-bottom: 2px;">
              {{ post.title }}
            </a>
          </h2>
          {% if post.excerpt %}
            <p style="margin: 0; color: #111; line-height: 1.7; font-size: 1.15rem; font-family: serif;">
              {{ post.excerpt | strip_html | truncatewords: 35 }}
            </p>
          {% endif %}
        </li>
      {% endfor %}
    </ul>

  </div>
</div>
