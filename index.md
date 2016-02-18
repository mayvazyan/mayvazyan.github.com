---
layout: page
title: Welcome!
tagline: Supporting tagline
---
{% include JB/setup %}

<ul class="entries">
            {% for post in site.posts limit:5 %}
              <li>
                <a href="{{ post.url }}">
                <h2>{{ post.title }}</h2>
		</a>
                <p class="blogdate">{{ post.date | date: "%d %B %Y" }}</p>
                <div>{{ post.content  }}</div>                
              </li>
            {% endfor %}
            </ul>

    
<ul class="posts">
  {% for post in site.posts offset:5 %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>


