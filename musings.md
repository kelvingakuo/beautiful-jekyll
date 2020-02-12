---
layout: page
title: Musings
subtitle: Interesting discoveries and lessons from work
---

<div class="posts-list">
  {% for post in site.categories.musings%}
  <article class="post-preview">
    {% if post.external-url %}
       <a href = "{{ post.external-url }}">
    {% else %}
      <a href="{{ post.url | prepend: site.baseurl }}">
    {% endif %}
	  <h2 class="post-title">{{ post.title | upcase }}</h2>

	  {% if post.subtitle %}
	  <h3 class="post-subtitle">
	    {{ post.subtitle }}
	  </h3>
	  {% endif %}
    </a>

    <p class="post-meta">
      <!-- Posted on {{ post.date | date: "%B %-d, %Y" }} -->
      {% assign words = content | number_of_words %}
      {% if words < 270 %}
        {{ 1 | plus: 2}} min read
      {% else %}
        {{ words | divided_by:135 | plus: 2 }} mins read
      {% endif %}
    </p>

    <div class="post-entry-container">
      {% if post.image %}
      <div class="post-image">
        <a href="{{ post.url | prepend: site.baseurl }}">
          <img src="{{ post.image }}">
        </a>
      </div>
      {% endif %}
      <div class="post-entry">
        {{ post.excerpt | strip_html | xml_escape | truncatewords: site.excerpt_length }}
        {% assign excerpt_word_count = post.excerpt | number_of_words %}

        {% if post.external-url %}
          <a href = "{{ post.external-url }}" class = "post-read-more">[READ&nbsp;MORE]</a>
        {% else %}
          {% if post.content != post.excerpt or excerpt_word_count > site.excerpt_length %}
            <a href="{{ post.url | prepend: site.baseurl }}" class="post-read-more">[READ&nbsp;MORE]</a>
          {% endif %}
        {% endif %}
      </div>
    </div>

    {% if post.tags.size > 0 %}
    <div class="blog-tags">
      Tags:
      {% if site.link-tags %}
      {% for tag in post.tags %}
      <a href="{{ site.baseurl }}/tags#{{- tag -}}">{{- tag -}}</a>
      {% endfor %}
      {% else %}
        {{ post.tags | join: ", " }}
      {% endif %}
    </div>
    {% endif %}

   </article>
  {% endfor %}
</div>