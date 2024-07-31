---
layout: page
title: Bargaining & cooperative game theory
description: Bargaining outcomes between one large and many small players
img: assets/img/voi/payoff_scatterplot_rounds_all.png
importance: 1
category: work
---

My PhD resesarch project examines the applicability of random order values, and more specifically, the Shapley value to the problem of modeling bargaining in a setting with one indispensable player and a large number of smaller, non-indispensable players. The project is motivated by platform economies, but the results are applicable to a wide range of settings.

The research resulted in three working papers:

 - **[The value of being indispensable: a cooperative approach to bargaining with a continuum of players](https://stanmart.github.io/ValueOfIntermediation/theory.pdf)**: An examination of the Shapley value in a setting with a small number of big players and a continuum of fringe players. The paper is an abstract, theoretical treatment of the problem.
 - **[Hybrid platforms and bargaining power](https://stanmart.github.io/ValueOfIntermediation/application.pdf)**: A more applied paper, which uses the Shapley value to model bargaining outcomes in a model of hybrid platforms. 
 - **[Characterizing Multiplayer Free-Form Bargaining: A Lab experiment](https://stanmart.github.io/unstructured-bargaining-analysis/paper.pdf)** (joint with Mia Lu): A lab experiment that examines the outcomes of bargaining and coalition formation in a setting with one indispensable and two smaller players.


## The value of being indispensable: a cooperative approach to bargaining with a continuum of players

This paper investigates the idea of using random order values, a concept from cooperative game theory, to model bargaining outcomes in games with one indispensable player and a continuum of fringe players.
I show that this approach proves to be very tractable, and leads to results that are in line with one's intuitive expectations about bargaining outcomes.
Thus, it can be a useful tool in modelling situations where one does not want to attribute all the bargaining power to one side of the market, and at the same time would like to avoid having to deal with an explicit multi-stage bargaining game.

The bargaining outcomes in the simplest model (Shapley value, one indispensable big player, non-heterogeneous fringe players) also have a nice, intuitive graphical representation.
Imagine that the big player and $$t$$ fraction of the fringe players can generate $$f(t)$$ total value.
Then, the total value can be represented by a rectanle with width 1 and height $$f(1)$$.
It turns out, that the big player gets the area of this rectangle which is below the graph of $$f(t)$$, while the fringe players share ther est equally.

<div class="row mt-2">
  <div class="col-sm mt-2 mt-md-0">
      {% include figure.html path="assets/img/voi/share_of_players_concave.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
  <div class="col-sm mt-2 mt-md-0">
      {% include figure.html path="assets/img/voi/share_of_players_concave.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
</div>

This captures the idea that the bargaining position of the big player is better when it is less important to have all fringe players on board, i.e. fringe players are more substitutable in a sense.


## Hybrid platforms and bargaining power

This paper explores the effects of a platform selling their own products in addition to acting as intermediaries (hybrid platform) in a setting when bargaining takes place between the platform and the potential entrants.
It highlights a so-far underappreciated aspect of hybrid platforms: having their own products increases their bargaining power over the other sellers.
This change in bargaining might lead to lower entry, and thus reduced product variety which in turn can have negative welfare consequences for the consumers.

The results show that when the platform has a larger product variety of its own, its bargaining power increases, and thus can obtain a larger share of total profits.
This in turn leads to less fringe entrants, a lower total product variety, and, ultimately, a decrease in consumer surplus.

<div class="row mt-2">
  <div class="col-sm mt-2 mt-md-0">
      {% include figure.html path="assets/img/voi/eq_number_of_firms.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
  <div class="col-sm mt-2 mt-md-0">
      {% include figure.html path="assets/img/voi/eq_consumer_surplus.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
</div>


## Characterizing Multiplayer Free-Form Bargaining: A Lab experiment

This paper examines the outcomes of bargaining and coalition formation in a setting with one indispensable and two smaller players.
We believe that this type of structure is representative of many real-world settings, such as an inventor who is in discussion with multiple investors for developing a new product.
Furthermore, we employ *free-form* bargaining in our experiment where bargaining takes place via chat, without any restrictions, aswWe believe this approach is much more realistic and captures relevant aspects of real-world bargaining.

<div class="row mt-3">
  <div class="col-sm mt-3 mt-md-0">
      {% include figure.html path="assets/img/voi/chat_1.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
  <div class="col-sm mt-3 mt-md-0">
      {% include figure.html path="assets/img/voi/chat_2.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
  <div class="col-sm mt-3 mt-md-0">
      {% include figure.html path="assets/img/voi/chat_3.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
</div>


We find support for the intuitive expectation, that the indispensable player can get a larger share of the total value when value of the small coalition, and thus the necessity of having both small players in the coalition, increases.
This is also in line with the theoretical predictions of the Shapley value and the nucleolus.
Upon closer inspection, we find that the nucleolus does better in terms of qualitative predictions, while none of the models are especially good at predicting the exact shares of the players in the treatments with high bargaining powe disparity.
In particular, the big player(s) get less than predicted, which might indicate that there are important fairness considerations that these solution concepts do not capture.
Furthermore, there is considerable heterogeneity in the outcomes, and thus possibly in players' (fairness) preferences.

<div class="row mt-2">
  <div class="col-sm mt-2 mt-md-0">
      {% include figure.html path="assets/img/voi/payoff_average_rounds_all.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
  <div class="col-sm mt-2 mt-md-0">
      {% include figure.html path="assets/img/voi/payoff_scatterplot_rounds_all.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
</div>

