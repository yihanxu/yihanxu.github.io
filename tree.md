---
layout: default
title:
permalink: /tree/
---
{% comment%}
Here we generate all the categories.
{% endcomment%}

{% assign rawcats = "" %}
{% for post in site.posts %}
{% assign tcats = post.category | join:'|' | append:'|' %}
{% assign rawcats = rawcats | append:tcats %}
{% endfor %}

{% assign rawcats = rawcats | split:'|' | sort %}

{% assign cats = "" %}

{% for cat in rawcats %}
{% if cat != "" %}

{% if cats == "" %}
{% assign cats = cat | split:'|' %}
{% endif %}

{% unless cats contains cat %}
{% assign cats = cats | join:'|' | append:'|' | append:cat | split:'|' %}
{% endunless %}
{% endif %}
{% endfor %}

<h1 class="page-title">
  <a href="#category-clouds">Category |</a> <a href="#tag-clouds">Tags</a>
</h1>
<br/>

<div class="posts" id="category-clouds">
<p>
{% for ct in cats %}
<a href="#{{ ct | slugify }}" class="codinfox-category-mark" style="color:#999;text-decoration: none;"> {{ ct }} </a> &nbsp;&nbsp;
{% endfor %}
<a href="#no-category" class="codinfox-category-mark" style="color:#999;text-decoration: none;"> No Category </a> &nbsp;&nbsp;
</p>

{% for ct in cats %}
<h2 id="{{ ct | slugify }}">{{ ct }}</h2>
<ul class="codinfox-category-list">
  {% for post in site.posts %}
  {% if post.category contains ct %}
  <li>
    <h3>
      <a href="{{ post.url }}">
        {{ post.title }} |
        <small>{{ post.date | date_to_string }}</small>
      </a>
<!--       {% for tag in post.tags %}
      <a class="codinfox-tag-mark" href="/blog/tag/#{{ tag | slugify }}">{{ tag }}</a>
      {% endfor %} -->
    </h3>
  </li>
  {% endif %}
  {% endfor %}
</ul>
{% endfor %}

<h2 id="no-category">No Category</h2>
<ul class="codinfox-category-list">
  {% for post in site.posts %}
  {% unless post.category %}
  <li>
    <h3>
      <a href="{{ post.url }}">
        {{ post.title }}
        <small>{{ post.date | date_to_string }}</small>
      </a>
      {% for tag in post.tags %}
      <a class="codinfox-tag-mark" href="/blog/tag/#{{ tag | slugify }}">{{ tag }}</a>
      {% endfor %}
    </h3>
  </li>
  {% endunless %}
  {% endfor %}
</ul>
</div>

{% comment%}
Here we generate all the tags.
{% endcomment%}

{% assign rawtags = "" %}
{% for post in site.posts %}
{% assign ttags = post.tags | join:'|' | append:'|' %}
{% assign rawtags = rawtags | append:ttags %}
{% endfor %}

{% assign rawtags = rawtags | split:'|' | sort %}

{% assign tags = "" %}

{% for tag in rawtags %}
{% if tag != "" %}

{% if tags == "" %}
{% assign tags = tag | split:'|' %}
{% endif %}

{% unless tags contains tag %}
{% assign tags = tags | join:'|' | append:'|' | append:tag | split:'|' %}
{% endunless %}
{% endif %}
{% endfor %}


<h1 class="page-title">
  <a href="#tag-clouds">Tags | </a><a href="#category-clouds">Category</a>
</h1>
<br/>

<div class="posts" id="tag-clouds">
<p>
{% for tag in tags %}
<a href="#{{ tag | slugify }}" class="codinfox-tag-mark"> {{ tag }} </a> &nbsp;&nbsp;
{% endfor %}

{% for tag in tags %}
<h2 id="{{ tag | slugify }}">{{ tag }}</h2>
<ul class="codinfox-category-list">
  {% for post in site.posts %}
  {% if post.tags contains tag %}
  <li>
    <h3>
      <a href="{{ post.url }}">
        {{ post.title }} |
        <small>{{ post.date | date_to_string }}</small>
      </a>
<!--       {% for tag in post.tags %}
      <a class="codinfox-tag-mark" href="/blog/tag/#{{ tag | slugify }}">{{ tag }}</a>
      {% endfor %} -->
    </h3>
  </li>
  {% endif %}
  {% endfor %}
</ul>
{% endfor %}

