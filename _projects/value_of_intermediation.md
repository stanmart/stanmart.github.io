---
layout: page
title: the value of intermediation
description: Bargaining outcomes between one large and many small players
img: assets/img/voi/project_pic.png
importance: 1
category: work
---

In my current research project, I am investigating the idea of using concepts from cooperative game theory (in particular, the Shapley-value) to model bargaining outcomes in games with a few large and a continuum of small players. The cooperative approach seems be a tractable alternative of explicitly modelling price structures and entry choices in platform settings. This approach might be advantageous when one does not want to attribute all the bargaining power to one type of market participants, and at the same time would like to avoid having to deal with an explicit multi-stage bargaining game.

Preliminary results show that

  - The outcomes of the Shapley-value-based gain sharing rule generally concur with intuitive expectations about bargaining outcomes.
  - Incorporating the cooperative bargaining procedure into larger, non-cooperative models is relatively straightforward
  - Even a simple hybrid platform model enhanced with such a bargaining procedure can yield novel, interesting results
  - Such models can beespecially relevant for upstream-downstream situations, platform settings, and two-sided markets.

A quick visual representation is the following. Imagine that without the platform, fraction $$t$$ of the firms can generate $$f_0(t)$$ total profits ($$f_0(t) = 0$$ in the first two pictures), while, with the platform, the total achievable profits are $$f(t)$$. If profits are shared according to Shapley-values, then the platform gets the blue area and firms get the red are. The results indicate, that (as one would probably expect) the firms get 

  - less when they are substitutes (left),
  - more when they are complements (middle),
  - more when the platform is not totally necessary (right).

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/voi/complements.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/voi/substitutes.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/voi/outside_option.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>

As of yet, there is no public working paper about this project. You can take a look [at this set of slides](https://stanmart.github.io/ValueOfIntermediation) instead. Also, if you would like to know more about the project, please [reach out](mailto:martin.stancsics@gmail.com). I am more than happy to discuss it.