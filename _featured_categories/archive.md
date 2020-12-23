---
# Featured tags need to have either the `list` or `grid` layout (PRO only).
layout: list

# The title of the tag's page.
title: Archive

# The name of the tag, used in a post's front matter (e.g. tags: [<slug>]).
slug: archive

# (Optional) Write a short (~150 characters) description of this featured tag.
#description: >
#  This is a featured category, which have their own page.
#  Check out `_featured_tags/example.md` to learn how to create your own.

#menu: true
# (Optional) You can disable grouping posts by date.
no_groups: true

# Exclude this example category from the sitemap.
# DON'T USE THIS SETTING IN YOUR CATEGORIES!
sitemap: false
---


#{% for category in site.categories %}
#  <h3>{{ category[0] }}</h3>
#  <ul>
#    {% for post in category[1] %}
#      <li><a href="{{ post.url }}">{{ post.title }}</a></li>
#    {% endfor %}
#  </ul>
#{% endfor %}
