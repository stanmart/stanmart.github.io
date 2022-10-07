---
layout: page
title: stress testing the banking system
description: Desiging an IFRS9 compliant stress testing framework
img: assets/img/stress_test/project_pic.png
importance: 2
category: work
---

During my central bank time, I worked at the department of applied research and stress testing. One of the most important recurring tasks of our group was performing the semi-annual banking system stress test. In a nutshell, we had to forecast the losses of each bank operating in Hungary in the case of a hypotethical macroeconomic downturn.

As a bank has many sources of income and potential losses, this task is highly complex, and requires a number of satellite models and the cooperation of multiple departments. (For an overview of the whole stress-testing procedure in 2014, take a look at [Stress testing at the Magyar Nemzeti Bank](https://www.mnb.hu/letoltes/op109-final.pdf) by Ádám Banai, Zsuzsanna Hosszút, Gyöngyi Körmendi, Sándor Sóvágó and Róbert Szegedi.) Because of this complexity, and the fact that it has been built step-by-step over many years, performing the calculations involved a large number of manual, non-automated steps (including compiling the starting databases, moving intermediate results between various software, making graphs by hand in Excel, etc.).

Starting from 2018, banks in Hungary were required to apply the [IFRS 9](https://www.ifrs.org/issued-standards/list-of-standards/ifrs-9-financial-instruments/) reporting standard when calculating their loan loss provisions. This created challenges for the top-down stress-test, as calculation (and forecast) of losses was much more complex under the new standard than before its introduction. We had to overhaul our most important satellite model: the one forecasting losses due to non-performing loans.

Together with Péter Lang, and with support from many of our colleagues, we have built a new loan loss provision forecast model from the ground up. Despite the computational difficulty, we have managed to create a model that is consistent with the new reporting standard's most important features. Unfortunately, as of yet, no research paper have been published about the model. Those who are interested in it can find some information in box 9 of the [November 2018 Financial Stability Report](https://www.mnb.hu/letoltes/financial-stability-report-nov-2018.pdf) or in [this presentation](https://www.eba.europa.eu/sites/default/documents/files/document_library/Calendar/Conference-Workshop/2019/8th%20annual%20workshop%20documents/10%20P%C3%A9ter%20Lang.pdf) given by Péter Lang.

<div class="row mt-2">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/stress_test/loan_losses.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/stress_test/comparison.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>

We also took this opportunity to automate many other parts of the stress testing process (e.g. automatic generation of SQL queries, a more ergonomic interface for model estimation), and to ensure better interoperability between the various parts of the task. By the end, the most important parts were migrated to R programs, easily able to communicate between each other. Furthermore, we switched to using S3 classes for our scripts, making it possible to use a consistent interface for various steps. Tasks, which required manual Excel intervention before (e.g. creating plots or calculating summaries) were also incorporated into the new R programs, and available through the same S3-based interface.
