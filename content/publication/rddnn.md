+++
title = "Guardians of the Deep Fog: Failure-Resilient DNN Inference from Edge to Cloud"
date = 2019-09-01T17:45:39-04:00
draft = false

# Authors. Comma separated list, e.g. `["Bob Smith", "David Jones"]`.
authors = ["Ashkan Yousefpour", "Siddartha Devic", "Brian Q. Nguyen", "Aboudy Kreidieh", "Alan Liao", "Alexandre M. Bayen", "Jason P. Jue"]

# Publication type.
# Legend:
# 0 = Uncategorized
# 1 = Conference paper
# 2 = Journal article
# 3 = Manuscript
# 4 = Report
# 5 = Book
# 6 = Book section
publication_types = ["1"]

# Publication name and optional abbreviated version.
publication = "Guardians of the Deep Fog: Failure-Resilient DNN Inference from Edge to Cloud"
publication_short = "Guardians of the Fog"

# Abstract and optional shortened version.
abstract = "Partitioning and distributing deep neural networks (DNNs) over physical nodes such as edge, fog, or cloud nodes, could enhance sensor fusion, and reduce bandwidth and inference latency. However, when a DNN is distributed over physical nodes, failure of the physical nodes causes the failure of the DNN units that are placed on these nodes. The performance of the inference task will be unpredictable, and most likely, poor, if the distributed DNN is not specifically designed and properly trained for failures. Motivated by this, we introduce deepFogGuard, a DNN architecture augmentation scheme for making the distributed DNN inference task failure-resilient. To articulate deepFogGuard, we introduce the elements and a model for the resiliency of distributed DNN inference. Inspired by the concept of residual connections in DNNs, we introduce skip hyperconnections in distributed DNNs, which are the basis of deepFogGuard's design to provide resiliency. Next, our extensive experiments using two existing datasets for the sensing and vision applications confirm the ability of deepFogGuard to provide resiliency for distributed DNNs in edge-cloud networks"
abstract_short = "We introduce deepFogGuard, a DNN architecture augmentation scheme for making the distributed DNN inference task failure-resilient. To articulate deepFogGuard, we introduce the elements and a model for the resiliency of distributed DNN inference. Inspired by the concept of residual connections in DNNs, we introduce skip hyperconnections in distributed DNNs, which are the basis of deepFogGuard's design to provide resiliency. Our extensive experiments using two existing datasets for the sensing and vision applications confirm the ability of deepFogGuard to provide resiliency for distributed DNNs in edge-cloud networks"

# Featured image thumbnail (optional)
image_preview = ""

# Is this a selected publication? (true/false)
selected = true

# Projects (optional).
#   Associate this publication with one or more of your projects.
#   Simply enter your project's filename without extension.
#   E.g. `projects = ["deep-learning"]` references `content/project/deep-learning.md`.
#   Otherwise, set `projects = []`.
projects = []

# Tags (optional).
#   Set `tags = []` for no tags, or use the form `tags = ["A Tag", "Another Tag"]` for one or more tags.
tags = ["Machine Learning", "Neural Networks", "Computer Networking"]

# Links (optional).
url_pdf = ""
url_preprint = "https://arxiv.org/abs/1909.00995"
url_code = "https://github.com/anrl-utd/clearShallowAtEase"
url_dataset = ""
url_project = ""
url_slides = ""
url_video = ""
url_poster = ""
url_source = ""

# Custom links (optional).
#   Uncomment line below to enable. For multiple links, use the form `[{...}, {...}, {...}]`.
# url_custom = [{name = "Custom Link", url = "http://example.org"}]

# Does this page contain LaTeX math? (true/false)
math = false

# Does this page require source code highlighting? (true/false)
highlight = true

# Featured image
# Place your image in the `static/img/` folder and reference its filename below, e.g. `image = "example.jpg"`.
[header]
image = ""
caption = ""

+++
