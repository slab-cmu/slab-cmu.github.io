---
layout: lab
title: slab
permalink: /slab/
subtitle: 
nav: true
horizontal: false

logo:
  align: left
  image: SLAB_inverse.svg
---

SLAB is the research group in the [Language Technologies Institute](https://www.lti.cs.cmu.edu/) at [CMU](https://www.cmu.edu/) led by [Emma Strubell](./about). We do research at the intersection of natural language processing (NLP) and machine learning. The high-level motivation for our work is democratizing AI (specifically, NLP). This means: 
- Everyone should be able to shape, and shape uses of, NLP technology, with or without access to substantial compute resources;
- The NLP community should provide text analysis solutions that are useful across a broad array of applications for solving real-world problems, not just tasks with the highest potential to increase capital. 

In SLAB we focus on research that pushes the NLP community towards these goals, which manifests in a variety of more specific research directions including:
- Efficient machine learning for NLP: training, fine-tuning, and inference.
- Transfer learning and generalization.
- NLP for expert domains such as scientific articles and legal text.
- Structured prediction.
- Ethical issues in ML and NLP.
<!-- You can learn more about Emma [here](./about). -->

<h2 class="post-title">
<b> Current students </b>
</h2>

<!-- pages/projects.md -->
<div class="projects">
{%- if site.enable_project_categories and page.display_categories %}
  <!-- Display categorized projects -->
  {%- for category in page.display_categories %}
  <h2 class="category">{{ category }}</h2>
  {%- assign categorized_projects = site.projects | where: "category", category -%}
  {%- assign sorted_projects = categorized_projects | sort: "importance" %}
  <!-- Generate cards for each project -->
  {% if page.horizontal -%}
  <div class="container">
    <div class="row row-cols-2">
    {%- for project in sorted_projects -%}
      {% include projects_horizontal.html %}
    {%- endfor %}
    </div>
  </div>
  {%- else -%}
  <div class="grid">
    {%- for project in sorted_projects -%}
      {% include projects.html %}
    {%- endfor %}
  </div>
  {%- endif -%}
  {% endfor %}

{%- else -%}
<!-- Display projects without categories -->
  {%- assign sorted_projects = site.projects | sort: "importance" -%}
  <!-- Generate cards for each project -->
  {% if page.horizontal -%}
  <div class="container">
    <div class="row row-cols-2">
    {%- for project in sorted_projects -%}
      {% include projects_horizontal.html %}
    {%- endfor %}
    </div>
  </div>
  {%- else -%}
  <div class="grid">
    {%- for project in sorted_projects -%}
      {% include projects.html %}
    {%- endfor %}
  </div>
  {%- endif -%}
{%- endif -%}
</div>
