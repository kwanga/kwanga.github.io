---
layout: home
title: Projects
permalink: /projects.html
---

<!-- 🛠️ THIS MANUALLY CREATES THE BEAUTIFUL YELLOW HEADER BLOCK -->
<header class="site-masthead" style="padding-bottom: 40px !important; min-height: auto !important; text-align: center; margin-bottom: 40px;">
  <div style="width: 100%; max-width: 820px; margin: 0 auto; padding: 0 20px; box-sizing: border-box;">
    <h1 class="content-title" style="margin-bottom: 20px; font-size: 2.2rem; font-weight: bold; border: none; color: #000;">Master Project Index</h1>
    
    <p style="font-size: 1.25rem; line-height: 1.8; color: #111; margin: 0 auto; font-family: serif; max-width: 720px;">
      Below is a complete index of the analytical models, data frameworks, and technical case studies I have built. Click any project title to read the full end-to-end breakdown.
    </p>
  </div>
</header>

<!-- 🛠️ MASTER INDEX LOOP LISTING ALL PROJECTS WITHOUT 3-PAGE LIMITS -->
<main class="home" id="main" role="main" aria-label="Content" style="max-width: 760px; margin: 0 auto; padding: 0 20px; box-sizing: border-box;">
  <ul class="post-list" style="list-style: none; padding: 0; margin: 0;">
    {% for post in site.posts %}
      <li style="margin-bottom: 40px; border-bottom: 1px dashed rgba(0,0,0,0.15); padding-bottom: 25px;">
        <span class="post-meta" style="font-size: 0.95rem; color: #666; display: block; margin-bottom: 8px; font-family: sans-serif;">
          {{ post.date | date: "%B %d, %Y" }}
        </span>
        <h2 style="margin: 0 0 12px 0; font-size: 1.75rem;">
          <a href="{{ post.url | relative_url }}" style="color: #000; text-decoration: none; font-weight: bold;">
            {{ post.title }}
          </a>
        </h2>
        {% if post.excerpt %}
          <p style="margin: 0; color: #333; line-height: 1.7; font-size: 1.1rem; font-family: serif;">
            {{ post.excerpt | strip_html | truncatewords: 35 }}
          </p>
        {% endif %}
      </li>
    {% empty %}
      <li style="text-align: center; color: #666; font-family: serif; font-size: 1.2rem; margin-top: 40px;">
        Case studies are currently pulling into production. Your data analytics workflows will display here shortly!
      </li>
    {% endfor %}
  </ul>
</main>