---
layout: page
title: Теги
tagline: "Архив всех постов, отсортированных по тегам."
---

{% capture site_tags %}{% for tag in site.tags %}{{ tag | first }}{% unless forloop.last %},{% endunless %}{% endfor %}{% endcapture %}
<!-- site_tags: {{ site_tags }} -->
{% assign tag_words = site_tags | split:',' | sort %}
<!-- tag_words: {{ tag_words }} -->

<div id="tags">
  <center>
  <ul class="tag-box inline">
  {% for item in (0..site.tags.size) %}{% unless forloop.last %}
    {% capture this_word %}{{ tag_words[item] | strip_newlines }}{% endcapture %}
    <a href="#{{ this_word | cgi_escape }}"><code class="tag"><nobr>{{ this_word }}&nbsp;<sup>{{ site.tags[this_word].size }}</sup></nobr></code></a>&nbsp;
  {% endunless %}{% endfor %}
  </ul>
  </center>

  {% for item in (0..site.tags.size) %}{% unless forloop.last %}
    {% capture this_word %}{{ tag_words[item] | strip_newlines }}{% endcapture %}
  <h2 id="{{ this_word | cgi_escape }}">{{ this_word }}</h2>
  <ul class="posts">
    {% for post in site.tags[this_word] %}{% if post.title != null %}
    <li itemscope><a href="{{ post.url }}">{{ post.title }}</a></li>
    {% endif %}{% endfor %}
  </ul>
  {% endunless %}{% endfor %}
</div>