---
layout: page
title: Can You Predict Love?
description: Speed dating analysis for MSDS Adv. Machine Learning (DATA-505)
img: /assets/img/ml_fp.png
redirect:
importance: 1
category: school
related_publications: false
---

[Christy Lawrence](https://cml-data.github.io/), Noelle Matthews, & Haleigh Schwartz

April 25, 2024

[GitHub Repo](https://github.com/schwartzh2017/Machine_learning_final_project)

Data from: [OpenML](https://www.openml.org/search?type=data&status=any&sort=runs&id=40536)


My partners, [Christy Lawrence](https://cml-data.github.io/), Noelle Matthews, and I worked together to analyze data from [OpenML](https://www.openml.org/search?type=data&status=any&sort=runs&id=40536) to determine what traits, if any, predict whether or not a couple will match after a speed dating round. We found the most important features in couples matching used preprocessors such as OneHotEncoder and StandardScaler, created ensemble models to predict which couples would match, and ran our data through unsupervised models like PCA and Kmeans to further refine our results. Please see our [code](https://github.com/schwartzh2017/Machine_learning_final_project) for more details. See below for a few sample images from our presentation.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/ml_fp_1.png" title="pca" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/ml_fp_2.png" title="confusion matrix" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/ml_fp_3.png" title="kmeans" class="img-fluid rounded z-depth-1" %}
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
