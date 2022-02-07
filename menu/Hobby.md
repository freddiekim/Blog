---

layout: page

title: Hobby

---

<ul class="posts">
  {% assign nyear = 2000 %}
  {% for post in site.categories.Hobby %}
    {% capture year %}{{ post.date | date: '%Y' }}{% endcapture %}
    {% if year != nyear%}
      {% assign nyear = year %}
      <h3>{{ post.date | date: '%Y' }}</h3>
    {% endif %}

    <li itemscope>
      <a href="{{ site.github.url }}{{ post.url }}">{{ post.title }}</a>
      <p class="post-date"><span><i class="fa fa-calendar" aria-hidden="true"></i> {{ post.date | date: "%B %-d" }} - <i class="fa fa-clock-o" aria-hidden="true"></i> {% include read-time.html %}</span></p>
    </li>
  {% endfor %}
</ul>
