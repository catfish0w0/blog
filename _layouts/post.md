---
# Mr. Green Jekyll Theme (https://github.com/MrGreensWorkshop/MrGreen-JekyllTheme)
# Copyright (c) 2022 Mr. Green's Workshop https://www.MrGreensWorkshop.com
# Licensed under MIT

layout: default
---

{%- include multi_lng/get-lng-by-url.liquid -%}
{%- assign lng = get_lng -%}
{%- include post_common/post-main.html post = page -%}

{% if site.data.conf.posts.comments.engine != empty
  and site.data.conf.posts.comments.engine != nil
  and page.comments_disable != true
%}
{% include post/comments.html %}
{% endif %}
