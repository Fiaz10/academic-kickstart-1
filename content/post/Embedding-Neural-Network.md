+++
title = "Embedding Neural Network"
date = 2018-08-21T15:44:43-05:00
draft = false

# Authors. Comma separated list, e.g. `["Bob Smith", "David Jones"]`.
authors = ["Sid Devic"]

# Tags and categories
# For example, use `tags = []` for no tags, or the form `tags = ["A Tag", "Another Tag"]` for one or more tags.
tags = []
categories = []

# Featured image
# Place your image in the `static/img/` folder and reference its filename below, e.g. `image = "example.jpg"`.
# Use `caption` to display an image caption.
#   Markdown linking is allowed, e.g. `caption = "[Image credit](http://example.org)"`.
# Set `preview` to `false` to disable the thumbnail in listings.
[header]
image = ""
caption = ""
preview = true

+++

Interpretable neural networks are currently nothing more then a pipe dream. However, if we were to make these machines even partially interpretable, maybe we could learn more about how they work.

[ Placeholder ]

Visually interpretable is a broad term. Here is a T-SNE embedding on the MNIST dataset, where 0's, 1's, etc. are clustered in their specified classes:
![T-SNE](/img/tsne.png)

## The Network
We wish to create a neural network that not only gives us a class prediction given an input image, but also a 3-dimensional embedding within a defined space. Furthermore, we want them to be clustered around "centers of confidence".
