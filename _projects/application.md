---
layout: page
title: Hybrid platforms and bargaining power
description: Exploring the effects of hybrid operation on bargaining power
img: assets/img/voi-application/main_pic.png
importance: 2
category: phd
---

My PhD resesarch project examines the applicability of random order values, and more specifically, the Shapley value to the problem of modeling bargaining in a setting with one indispensable player and a large number of smaller, non-indispensable players.
The project is motivated by platform economies, but the results are applicable to a wide range of settings.
The repository for the thesis, as well as the three chapters, can be found at [stanmart/phd-thesis](https://github.com/stanmart/phd-thesis).

This chapter presents a model of a hybrid platform, which engages in bargaining with the fringe entrants.
It uses the Shapley value to model bargaining outcomes in tractable but not overly simplistic manner. 

 - Paper: [Hybrid platforms and bargaining power](https://stanmart.github.io/phd-thesis/application.pdf)
 - Archived Github repository: [stanmart/ValueOfIntermediation](https://stanmart.github.io/ValueOfIntermediation)


## Hybrid platforms and bargaining power

This paper explores the effects of a platform selling their own products in addition to acting as intermediaries (hybrid platform) in a setting when bargaining takes place between the platform and the potential entrants.
It highlights a so-far underappreciated aspect of hybrid platforms: having their own products increases their bargaining power over the other sellers.
The results show that when the platform has a larger product variety of its own, its bargaining power increases, and thus can obtain a larger share of total profits. This in turn leads to less fringe entrants.

{% include figure.html path="assets/img/voi-application/eq_change.png" class="img-fluid rounded z-depth-1" zoomable=true width=600 %}

As it turns out, even within an otherwise frictionless setting (most notably, lump-sum platform entry fees), the decrease in fringe entry is so large that it is not compensated by the increase in the platform's own product variety.
This in turn leads to a lower total product variety, and, ultimately, a decrease in consumer surplus.

<div class="row mt-2">
  <div class="col-sm mt-2 mt-md-0">
      {% include figure.html path="assets/img/voi-application/eq_number_of_firms.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
  <div class="col-sm mt-2 mt-md-0">
      {% include figure.html path="assets/img/voi-application/eq_consumer_surplus.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
</div>

These results demonstrate that there is a so far underapppreciated aspect of the hybrid operation of platforms.
Namely, platform's having their own products increases their bargaining power, which might change how profits are divided between the platform and the fringe entrants.
Under certain conditions, can lead to a decrease in consumer surplus.
