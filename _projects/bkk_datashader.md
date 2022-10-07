---
layout: page
title: Visualizing public transport
description: An exploration of visualizing large datasets
img: assets/img/bkk/project_pic.png
importance: 1
category: fun
---

Sometime in 2018, I came across the Python library called [`datashader`](https://datashader.org/). It has the aim of creating scatterplots of large datasets in a performant but still meaningful way. When coming across some new tool, I like to incorporate it in some small demo project, as I found that hands-on learning works best for me. That is what I did with `datashader`.

The idea is simple: the Centre for Budapest Transport (BKK) provides (or, at least, used to provide) an API for accessing the location of all of its vehicles in real time. All I did was to query the location of all vehicles at a regular interval, for 24 hours. After that, I created a scatterplot of the recorded locations. I have also overlaid this scatterplot on an interactive, zoomable map of the city.

I learned a lot while doing this project. If you are interested, head over to [my blog post about it]({% post_url 2018-10-17-bkk-datashader %}) where I write about the process in more detail. Also, I think the resulting plots are quite nice. You can take a look at them below.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/bkk/BUD_schedule_fire.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/bkk/BUD_gps_fire.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/bkk/BUD_gps_by_type.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
