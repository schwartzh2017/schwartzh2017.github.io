---
layout: page
title: GitHub Repos Survivability 
description: Analysis of survivability of GitHub repos for MSDS Survival Analysis (DATA-596)

img: /assets/img/survival_analysis_final_project_km_curve.png
redirect:
importance: 2
category: school
related_publications: false
---

[Nick Brooks](https://nickbrooks-ds.github.io/) & Haleigh Schwartz

April 24, 2024

[Google slides presentation](https://docs.google.com/presentation/d/1ihUJ366En04LmeBpgqHGs5y6o8plJnn4DxuPwu6vbLs/edit?usp=sharing)

[GitHub Repo](https://github.com/schwartzh2017/Survival_Project3)

Data from: [A. Ait, J. L. C. Izquierdo and J. Cabot, "An Empirical Study on the Survival Rate of GitHub Projects," 2022 IEEE/ACM 19th International Conference on Mining Software Repositories (MSR), Pittsburgh, PA, USA, 2022, pp. 365-375, doi: 10.1145/3524842.3527941.](https://ieeexplore.ieee.org/document/9796216)


My partner, [Nick Brooks](https://nickbrooks-ds.github.io/), and I worked together to analyze data from ["An Empirical Study on the Survival Rate of GitHub Projects,"](https://ieeexplore.ieee.org/document/9796216) to investigate survivability of GitHub repositories. We created KM curves, fit out data to various custom models, discovered traits of surviving repositories, and predicted the mean lifetime of repos based on those traits. Please see our [code](https://github.com/schwartzh2017/Survival_Project3) and [Google slides presentation](https://docs.google.com/presentation/d/1ihUJ366En04LmeBpgqHGs5y6o8plJnn4DxuPwu6vbLs/edit?usp=sharing) for more details. See below for a few sample images from our presentation.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/sa_fp_ex1.png" title="survival probability over time per ecosystem" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/sa_fp_ex3.png" title="weibull plot" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/sa_fp_ex2.png" title="survival probability over time per triad" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

<!-- {% raw %}

```html
<div class="row justify-content-sm-center">
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm-4 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
```

{% endraw %} -->
