<nav class="site-navigation" style="display: flex; justify-content: space-between; align-items: center; width: 100%; max-width: 820px; margin: 0 auto; padding: 15px 20px; box-sizing: border-box; font-family: sans-serif;">
  
  <!-- 🛠️ DYNAMIC HISTORICAL BACK BUTTON (ONLY HIDES ON THE MAIN HOMEPAGE) -->
  <div class="back-navigation">
    {% if page.url != "/" and page.url != "/index.html" %}
      <a href="javascript:history.back()" style="color: #000; text-decoration: none; font-weight: bold; font-size: 0.9rem; display: flex; align-items: center; gap: 5px; background: rgba(0,0,0,0.04); border: 1px solid rgba(0,0,0,0.12); padding: 6px 14px; border-radius: 4px;" title="Go back">
        <span>←</span> Back
      </a>
    {% else %}
      <span>&nbsp;</span>
    {% endif %}
  </div>

  <!-- RIGHT SIDE: PREMIUM CLICKABLE NAVIGATION TABS -->
  <div class="menu-links" style="display: flex; gap: 10px;">
    {% for item in site.data.menu %}
      <a href="{{ item.url | relative_url }}" style="text-decoration: none; font-weight: bold; font-size: 0.9rem; padding: 6px 14px; border-radius: 4px; transition: all 0.2s ease; font-family: sans-serif; display: inline-block; white-space: nowrap;
        {% if page.url == item.url or page.url == '/index.html' and item.url == '/' or page.url == '/' and item.url == '/' %}
          background-color: #000000; color: #ffffff; border: 1px solid #000000;
        {% else %}
          background-color: transparent; color: #000000; border: 1px solid rgba(0,0,0,0.15);
        {% endif %}">
        {{ item.title }}
      </a>
    {% endfor %}
  </div>

</nav>
