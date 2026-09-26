---
layout: default
title: Projects
permalink: /projects.html
---

<div style="background-color: #f5c71a; min-height: 100vh; width: 100%; display: block; margin: 0; padding: 40px 0; box-sizing: border-box;">
  
  <div style="width: 100%; max-width: 800px; margin: 0 auto; padding: 0 20px; box-sizing: border-box;">
    
    <div style="text-align: center; margin-bottom: 30px;">
      <h1 style="font-size: 2.2rem; font-weight: bold; color: #000; margin-bottom: 15px; font-family: serif;">Master Project Index</h1>
      <p style="font-size: 1.2rem; line-height: 1.7; color: #111; font-family: serif; max-width: 680px; margin: 0 auto;">
        Click any project title to open up its interactive presentation deck slide gallery.
      </p>
    </div>

    <!-- Clickable project block lists linking to individual posts -->
    <ul style="list-style: none; padding: 0; margin: 0;">
      {% for post in site.posts %}
        <li style="margin-bottom: 25px;">
          <a href="{{ post.url | relative_url }}" style="text-decoration: none; color: #000; display: block; background: #000000; border: 1px solid #111; border-radius: 6px; padding: 25px; box-shadow: 0 4px 12px rgba(0,0,0,0.15);">
            <div style="display: flex; justify-content: space-between; align-items: flex-start; margin-bottom: 10px;">
              <h2 style="margin: 0; font-size: 1.45rem; color: #ffffff; font-weight: bold; font-family: sans-serif;">
                {{ post.title }}
              </h2>
              <span style="font-size: 0.85rem; color: #f5c71a; font-family: sans-serif; font-weight: bold;">
                {{ post.date | date: "%B %d, %Y" }}
              </span>
            </div>
            <div style="margin-top: 15px; text-align: right; font-size: 0.9rem; color: #f5c71a; font-weight: bold; font-family: sans-serif;">
              Open Presentation Slides →
            </div>
          </a>
        </li>
      {% endfor %}
    </ul>

  </div>
</div>
