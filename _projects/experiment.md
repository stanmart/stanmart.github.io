---
layout: page
title: Characterizing Multiplayer Free-Form Bargaining
description: A Lab experiment
img: assets/img/voi-experiment/payoff_averages_rounds_all.png
importance: 3
category: phd
---

My PhD resesarch project examines the applicability of random order values, and more specifically, the Shapley value to the problem of modeling bargaining in a setting with one indispensable player and a large number of smaller, non-indispensable players.
This chapter presents a lab experiment that examines the outcomes of bargaining and coalition formation in a setting with one indispensable and two smaller players.

 - Paper: [Characterizing Multiplayer Free-Form Bargaining: A Lab experiment](https://stanmart.github.io/unstructured-bargaining-analysis/paper.pdf) (joint with Mia Lu)
 - Github repository for the experiment: [stanmart/unstructured-bargaining-experiment](https://stanmart.github.io/unstructured-bargaining-experiment)
 - Github repository for the replication package: [stanmart/unstructured-bargaining-analysis](https://stanmart.github.io/unstructured-bargaining-analysis)

## Characterizing Multiplayer Free-Form Bargaining: A Lab experiment

This paper examines the outcomes of bargaining and coalition formation in a setting with one indispensable and two smaller players.
We believe that this type of structure is representative of many real-world settings, such as an inventor who is in discussion with multiple investors for developing a new product.
Furthermore, we employ *free-form* bargaining in our experiment where bargaining takes place via chat, without any restrictions, aswWe believe this approach is much more realistic and captures relevant aspects of real-world bargaining.

<div class="row mt-3">
  <div class="col-sm mt-3 mt-md-0">
      {% include figure.html path="assets/img/voi-experiment/chat_1.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
  <div class="col-sm mt-3 mt-md-0">
      {% include figure.html path="assets/img/voi-experiment/chat_2.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
  <div class="col-sm mt-3 mt-md-0">
      {% include figure.html path="assets/img/voi-experiment/chat_3.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
</div>


We find support for the intuitive expectation, that the indispensable player can get a larger share of the total value when value of the small coalition, and thus the necessity of having both small players in the coalition, increases.
This is also in line with the theoretical predictions of the Shapley value and the nucleolus.
Upon closer inspection, we find that the nucleolus does better in terms of qualitative predictions, while none of the models are especially good at predicting the exact shares of the players in the treatments with high bargaining powe disparity.
In particular, the big player(s) get less than predicted, which might indicate that there are important fairness considerations that these solution concepts do not capture.
Furthermore, there is considerable heterogeneity in the outcomes, and thus possibly in players' (fairness) preferences.

<div class="row mt-2">
  <div class="col-sm mt-2 mt-md-0">
      {% include figure.html path="assets/img/voi-experiment/payoff_average_rounds_all.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
  <div class="col-sm mt-2 mt-md-0">
      {% include figure.html path="assets/img/voi-experiment/payoff_scatterplot_rounds_all.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
</div>

