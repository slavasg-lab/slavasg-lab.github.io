---
layout: about
title: about
permalink: /

profile:
  align: right
  image: prof_pic.jpg
  image_circular: false # crops the image to make it circular
  # more_info: >
  #   <p>555 your office number</p>
  #   <p>123 your address street</p>
  #   <p>Your City, State 12345</p>

selected_papers: false # publications are included in the page body below, with our own heading
social: false # includes social icons at the bottom of the page

announcements:
  enabled: false # news is included in the page body below (limit/scrollable still apply)
  scrollable: true # adds a vertical scroll bar if there are more than 3 news items
  limit: 5 # leave blank to include all the news in the `_news` folder

latest_posts:
  enabled: false
  scrollable: true # adds a vertical scroll bar if there are more than 3 new posts items
  limit: 3 # leave blank to include all the blog posts
---

B.Sc. Mechanical Engineering, RWTH Aachen (2026). Currently boosting shareholder value at [Papaia Innovation](https://papaia.ch).

During my bachelor's I did research on learning-based control and robot learning at the Max Planck Institute for Intelligent Systems,
ETH Zürich and TU Dresden. In general, I'm interested in intelligence in physical systems and the many forms it can take.

Outside of work I like being outdoors, hiking or biking somewhere. On longer trips that usually involves freezing in a tent and promising never to
do that to myself again.

<h2>
  <a href="{{ '/news/' | relative_url }}" style="color: inherit">news</a>
</h2>

{% include news.liquid limit=true %}

<h2>
  <a href="{{ '/publications/' | relative_url }}" style="color: inherit">publications</a>
</h2>

{% include selected_papers.liquid %}

<h2>
  <a href="{{ '/projects/' | relative_url }}" style="color: inherit">projects</a>
</h2>

<div class="projects">
  <div class="row row-cols-1 row-cols-md-3">
    {% assign sorted_projects = site.projects | sort: "importance" %}
    {% for project in sorted_projects %}
      {% include projects.liquid %}
    {% endfor %}
  </div>
</div>
