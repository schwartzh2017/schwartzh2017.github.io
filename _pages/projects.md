---
layout: page
title: projects
permalink: /projects/
description:
nav: true
nav_order: 3
display_categories: [Synodi, InterWorks, Main Street Family Medicine, New Heights Clinic, Willamette University]
category_intros:
  Synodi: |
    [Synodi](https://synodi.app) is the mobile app I founded and built: a trip companion and expense splitter in one, available now on iOS and Android.
  InterWorks: |
    As an analytics consultant at [InterWorks](https://interworks.com), I partner directly with clients to build data products and shape their analytics strategy. Because that work belongs to my clients, I can't showcase it here, but the highlights include:

    - Designing and deploying end-to-end analytics solutions with Sigma, Claude, Databricks, dbt, and Tableau
    - Turning ambiguous business problems into clear, actionable data products
    - Supporting BI tool migrations and advising on modern analytics architecture
    - Writing technical blogs, co-hosting webinars, and earning certifications to stay sharp on the tools I consult in

    Below are some of the blogs and webinars I've published with InterWorks.
  Main Street Family Medicine: |
    At [Main Street Family Medicine](https://www.mainstreetfamilymed.com/), I started as a medical assistant and grew into the clinic's data analyst and office manager. There I:

    - Built automated scripts to analyze healthcare and company financial data
    - Developed custom applications for the clinic's unique business model
    - Managed the clinic website and launched ongoing staff training initiatives

    Some reports are partially concealed below to protect patient and business confidentiality.
  New Heights Clinic: |
    As the data analyst and project manager at [New Heights Clinic](https://newheights.org/new-heights-clinic/), a nonprofit clinic, I helped the clinic grow by:

    - Analyzing patient data in depth to tailor services to community needs
    - Implementing the clinic's first Electronic Medical Record (transitioning from paper charts)
    - Analyzing and improving clinic processes for more efficient, higher-quality care
  Willamette University: |
    Projects from my Master's in [Data Science at Willamette University](https://willamette.edu/academics/computing/data-science/), spanning machine learning, survival analysis, and my capstone on healthcare access in the United States.
horizontal: false
---

<!-- pages/projects.md -->
<div class="projects">
{% if site.enable_project_categories and page.display_categories %}
  <!-- Display categorized projects -->
  {% for category in page.display_categories %}
  <a id="{{ category }}" href=".#{{ category }}">
    <h2 class="category">{{ category }}</h2>
  </a>
  {% if page.category_intros[category] %}
  <div class="mb-4">{{ page.category_intros[category] | markdownify }}</div>
  {% endif %}
  {% assign categorized_projects = site.projects | where: "category", category %}
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

{% assign sorted_projects = site.projects | sort: "importance" %}

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
