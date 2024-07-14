---
layout: page
title: Monthly Reports Application
description: Customizable monthly reports for Main Street Family Medicine, PLLC.
img: assets/img/ppd_ex.png
redirect:
importance: 1
category: work
related_publications: false
---

While I cannot link back to my source code due to confidentiality reasons, I created an application to run monthly reports for [Main Street Family Medicine](https://www.mainstreetfamilymed.com/). I wrote scripts for easily extracting data from our Electronic Medical Record (EMR) and re-running pertinent analyses each month. Using tools such as Quarto, Netlify, Web-R, and Shiny, I merged these reports into a publishable (yet private) application for internal sharing. 

The example below is an image of an interactive report I titled "PPD" ("Patients Per Day"). The user can toggle between provider, date, and what type of day that provider worked (full, part, or all types of days). The rendered plotly depicts not only the selected features but also the average between those same time points and types of days for all providers working. The user can hover over any specific point to see more details for all providers from that same day. 

Other reports I run analyze our financial and patient data. Work with patient data is helpful to both our nurse practitioner students as they work on their doctorate projects and the rest of our staff as we continually seek to provide relevant and effective care for our patients. The business reports are especially important in making informed decisions for the future of our clinic as we are transitioning to cover a provider on maternity leave, actively gaining patients, and on-boarding new providers and staff.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/ppd_ex.png" title="ppd" class="img-fluid rounded z-depth-1" %}
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
