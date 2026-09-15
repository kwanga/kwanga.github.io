---
layout: default
title: Projects
permalink: /projects.html
---

<div style="background-color: #f2c811; min-height: 100vh; width: 100%; display: block; margin: 0; padding: 0 0 60px 0; box-sizing: border-box; clear: both;">
  
  <!-- 🛠️ INJECTED CLEAN TOP HEADER BACK BUTTON STRIP -->
  <nav style="display: flex; justify-content: space-between; align-items: center; width: 100%; max-width: 820px; margin: 0 auto; padding: 15px 20px; box-sizing: border-box; font-family: sans-serif;">
    <div class="back-navigation">
      <a href="javascript:history.back()" style="color: #000; text-decoration: none; font-weight: bold; font-size: 0.9rem; display: flex; align-items: center; gap: 5px; background: rgba(0,0,0,0.04); border: 1px solid rgba(0,0,0,0.12); padding: 6px 14px; border-radius: 4px;" title="Go back">
        <span>←</span> Back
      </a>
    </div>
    <span>&nbsp;</span>
  </nav>

  <!-- MAIN CANVAS CONTENT WRAPPER -->
  <div style="width: 100%; max-width: 800px; margin: 0 auto; padding: 0 20px; box-sizing: border-box;">
    
    <!-- HEADER SUMMARY -->
    <div style="text-align: center; margin-bottom: 5px; margin-top: 10px;">
      <h1 style="font-size: 2.2rem; font-weight: bold; color: #000; margin-bottom: 15px; font-family: serif; border: none;">Master Project Index</h1>
      <p style="font-size: 1.2rem; line-height: 1.7; color: #111; font-family: serif; max-width: 680px; margin: 0 auto;">
        Below is a complete index of the analytical models, data frameworks, and technical case studies I have built. Click any project title to read the full end-to-end breakdown.
      </p>
    </div>

    <!-- 🛠️ PREMIUM VERTICAL CLICKABLE TABS LOOP FOR CASES -->
    <ul class="post-list" style="list-style: none; padding: 0; margin: 40px 0 0 0;">
      {% for post in site.posts %}
        <li style="margin-bottom: 25px; box-sizing: border-box;">
          <a href="{{ post.url | relative_url }}" style="text-decoration: none; color: #000; display: block; background: #000000; border: 1px solid #111; border-radius: 6px; padding: 25px; box-shadow: 0 4px 12px rgba(0,0,0,0.15); transition: transform 0.2s ease;">
            
            <div style="display: flex; justify-content: space-between; align-items: flex-start; margin-bottom: 10px; flex-wrap: wrap; gap: 5px;">
              <h2 style="margin: 0; font-size: 1.45rem; color: #ffffff; font-weight: bold; font-family: sans-serif; border: none; padding: 0;">
                {{ post.title }}
              </h2>
              <span style="font-size: 0.85rem; color: #f2c811; font-family: sans-serif; font-weight: bold; background: rgba(242, 200, 17, 0.1); border: 1px solid rgba(242, 200, 17, 0.25); padding: 4px 10px; border-radius: 4px; white-space: nowrap;">
                {{ post.date | date: "%B %d, %Y" }}
              </span>
            </div>

            {% if post.excerpt %}
              <p style="margin: 0; color: #cccccc; line-height: 1.6; font-size: 1rem; font-family: serif;">
                {{ post.excerpt | strip_html | truncatewords: 30 }}
              </p>
            {% endif %}
            
            <div style="margin-top: 15px; text-align: right; font-size: 0.9rem; color: #f2c811; font-weight: bold; font-family: sans-serif;">
              Read Case Study Details →
            </div>

          </a>
        </li>
      {% endfor %}
    </ul>

  </div>
</div>
