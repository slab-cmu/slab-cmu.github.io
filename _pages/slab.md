---
layout: lab
title: slab
permalink: /slab/
subtitle: 
nav: true
display_categories: ["Current students", "Alumni"]

logo:
  align: left
  image: SLAB_inverse.jpeg
---

SLAB is the research group in the [Language Technologies Institute](https://www.lti.cs.cmu.edu/) at [CMU](https://www.cmu.edu/) led by [Emma Strubell](/). We do research at the intersection of natural language processing (NLP) and machine learning. The high-level motivation for our work is democratizing AI (specifically, NLP). This means: 
- Everyone should be able to shape, and shape uses of, NLP technology, with or without access to substantial computational or financial resources;
- The NLP community should provide text analysis solutions that are useful across a broad array of applications for solving real-world problems, not just tasks with the highest potential to increase capital. 

In SLAB we focus on research that pushes the NLP community towards these goals, which manifests in a variety of more specific research directions including:
- Efficient machine learning for NLP: training, fine-tuning, and inference.
- Data efficiency: transfer learning and generalization.
- NLP for expert domains such as scientific articles and legal text.
- Structured prediction.
- Ethical and policy concerns in ML and NLP.
<!-- You can learn more about Emma [here](./about). -->

<!-- <h2 class="post-title">
<b> Current students </b>
</h2> -->

<!-- pages/projects.md -->
<div class="projects">
{% if site.enable_project_categories and page.display_categories %}
  <!-- Display categorized projects -->
  {% for category in page.display_categories %}
  <a id="{{ category }}" href=".#{{ category }}">
    <h2 class="category">{{ category }}</h2>
  </a>
  {% assign categorized_projects = site.students | where: "category", category %}
  {% assign sorted_projects = categorized_projects | sort: "importance" %}
  <!-- Generate cards for each project -->
  {% if page.horizontal %}
  <div class="container">
    <div class="row row-cols-1 row-cols-md-2">
    {% for project in sorted_projects %}
      {% include projects_horizontal.liquid %}
    {% endfor %}
    </div>
  </div>
  {% else %}
  <div class="row row-cols-1 row-cols-md-3">
    {% for project in sorted_projects %}
      {% include projects.liquid %}
    {% endfor %}
  </div>
  {% endif %}
  {% endfor %}

{% else %}

<!-- Display projects without categories -->

{% assign sorted_projects = site.students | sort: "importance" %}

  <!-- Generate cards for each project -->

{% if page.horizontal %}

  <div class="container">
    <div class="row row-cols-1 row-cols-md-2">
    {% for project in sorted_projects %}
      {% include projects_horizontal.liquid %}
    {% endfor %}
    </div>
  </div>
  {% else %}
  <div class="row row-cols-1 row-cols-md-3">
    {% for project in sorted_projects %}
      {% include projects.liquid %}
    {% endfor %}
  </div>
  {% endif %}
{% endif %}
</div>
