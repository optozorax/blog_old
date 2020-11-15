---
layout: page
title: Теги
tagline: "Архив всех постов, отсортированных по тегам."
---

{% assign submodules = site.pages | where: "submodule", true %}
{% capture site_tags %}{% for tag in site.tags %}{{ tag | first }}{% unless forloop.last %},{% endunless %}{% endfor %}{% endcapture %}
{% assign pages_tags = submodules | map: "tags" %}
{% capture pages_tags1 %}{% for tag_array in pages_tags %}{% for tag in tag_array %}{{ tag }},{% endfor %}{% endfor %}{% endcapture %}
{% assign tag_words = pages_tags1 | append: site_tags | split: "," | sort | uniq %}

<div id="tags">
  <center>
  <ul class="tag-box inline">
  {% for this_word in tag_words %}
    {% assign size = site.tags[this_word].size | default: 0 %}
    {% for array in pages_tags %}
      {% for item in array %}
        {% if item == this_word %}
          {% assign size = size | plus: 1 %}
        {% endif %}
      {% endfor %}
    {% endfor %}
    <a href="#{{ this_word | cgi_escape }}"><code class="tag"><nobr>{{ this_word }}&nbsp;<sup>{{ size }}</sup></nobr></code></a>&nbsp;
  {% endfor %}
  </ul>
  </center>

  {% for this_word in tag_words %}
  <h2 id="{{ this_word | cgi_escape }}">{{ this_word }}</h2>
  <ul class="posts">
    {% if site.tags contains this_word %}
      {% for post in site.tags[this_word] %}{% if post.title != null %}
      <li itemscope><a href="{{ post.url }}">{{ post.title }}</a></li>
      {% endif %}{% endfor %}
    {% endif %}
    {% for page in submodules %}
      {% if page.tags contains this_word %}
        <li itemscope><a href="{{ page.url }}">{{ page.title }}</a></li>
      {% endif %}
    {% endfor %}
  </ul>
  {% endfor %}
</div>