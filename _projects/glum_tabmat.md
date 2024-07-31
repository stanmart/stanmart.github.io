---
layout: page
title: User-friendly GLMs with Glum 3
description: High-performance and user-friendly GLM estimation in Python
img: assets/img/glum-tabmat/main_pic.png
importance: 1
category: work
---

*[glum](https://github.com/Quantco/glum)* is a lightning fast Python package for estimating Generalized Linear Models (GLMs).
It can handle mixed sparsity (dense, sparse and categorical) data in a memory and computationally efficient way.
My main task during my 2023 internship at [QuantCo](https://quantco.com/) was to improve glum, and its backend library, *[tabmat](https://github.com/Quantco/tabmat)* even further.

glum follows scikit-learn's API conventions, so it is easily composable with other tools.
However, many people with a statistics or econometrics background are rather used to formula interfaces, such as the ones provided by R's glm or Python's statsmodels packages.
To make glum more user-friendly for these users, and more suitable for exploratory analysis, I developed a formula interface for glum, based on the fantastic [formulaic](https://matthewwardrop.github.io/formulaic/) library.
Since th v3 release, glum can now do the following:

```python
model = glum.GeneralizedLinearRegressor(
    formula=(
        "Miles_per_Gallon ~ Weight_in_lbs + {Weight_in_lbs**2} "
        "+ bs(Horsepower, 3) + C(Cylinders) * Origin"
    ),
    store
    alpha=0,
)
model.fit(cars[:380], store_covariance_matrix=True)

pred = model.predict(cars[380:])

```

True to glum's spirit, the formula interface was also designed with performance in mind.
In particular, variable interactions preserve sparsity (the interaction of a dense and a sparse column will always be sparse), and glum uses this fact to save memory.
Furthermore, glum exploits the observation that the interaction of any two categoricals can be represented as one new categorical.
This makes it possible to include interactions with high-cardinality categoricals in models without worrying about memory implications.
For example, the following code snippet should run without problems on an average computer.

```python
df = pd.DataFrame(
    {
        "c1": pd.Categorical(np.random.randint(low=1, high=200, size=1_000_000)),
        "c2": pd.Categorical(np.random.randint(low=1, high=200, size=1_000_000)),
        "y": np.random.rand(1_000_000),
    }
)
big_model = glum.GeneralizedLinearRegressor(formula="y ~ c1 : c2", alpha=1).fit(df)
```

While the formula interface is the highlight of glum's v3 release (and tabmat's v4 release), there are a number of other improvements as well.
These include more flexible variable (and term) names, easy-to-use Wald tests, and a more flexible handing of missing values in categorical columns.
The following snippet shows the different ways to perform a Wald test in glum.
```python
model.wald_test(features=["Weight_in_lbs", "Weight_in_lbs ** 2"], r=[0, 0])
model.wald_test(terms=["bs(Horsepower, 3)"], r=[0])
model.wald_test(formula="-2 * Weight_in_lbs = `Weight_in_lbs ** 2`")
```

tabmat also went through a refactoring to unify its API, and make it easier to improve and maintain in the future without breaking changes.
It can now also store column and term names for the various matrix types it supports, bringing it closer to the vision of being in-between matrix libraries like numpy and full-fledged dataframes like pandas or polars.


For more details, check out the following links:

 - [Quantco tech blog post about the release](https://tech.quantco.com/blog/glum-v3)
 - [Example notebook showcasing the formula interface](https://glum.readthedocs.io/en/latest/tutorials/formula_interface/formula_interface.html#)
 - [glum v3 release notes](https://github.com/Quantco/glum/releases/tag/v3.0.0)
 - [tabmat v4 release notes](https://github.com/Quantco/tabmat/releases/tag/4.0.0)
