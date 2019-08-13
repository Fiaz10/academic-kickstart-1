+++
title = "Iterative Piecewise Convex Function Fitting"
date = 2018-09-18T20:31:34-05:00
draft = true

# Tags: can be used for filtering projects.
# Example: `tags = ["machine-learning", "deep-learning"]`
tags = ["research", "machine-learning", "convex-optimization"]

# Project summary to display on homepage.
summary = "Developing an iterative piecewise-convex function fitting algorithm for prediction on regression tasks. Mentored by Prof. Nicholas Ruozzi, UTD. Python, cvxpy, MATLAB."

# Optional image to display on homepage.
image_preview = "pwcvx.png"

# Optional external URL for project (replaces project detail page).
external_link = ""

# Does the project detail page use math formatting?
math = true

# Does the project detail page use source code highlighting?
highlight = true

# Featured image
# Place your image in the `static/img/` folder and reference its filename below, e.g. `image = "example.jpg"`.
[header]
image = ""
caption = ""

+++
_Work in progress, code available [here](https://github.com/sid-devic/cvx). Sorry for no documentation!_
Test proj, please ignore
Fitting a convex piecewise linear function to a given set of data can be done using the algorithm described in [Boyd and Vandenberghe, 338]:
$$ {\min_{x\in S} f(x)} $$
\begin{aligned}
& \underset{x}{\text{minimize}}
& & f_1(x) \newline
& \text{subject to}
& & f_i(x) \leq b_i, \; i = 1, \ldots, m.
\end{aligned}
