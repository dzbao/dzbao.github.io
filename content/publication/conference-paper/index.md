---
title: 'GNNs as Adapters for LLMs on Text-Attributed Graphs'

# Authors
# If you created a profile for a user (e.g. the default `admin` user), write the username (folder name) here
# and it will be replaced with their full name and linked to their profile.
authors:
  - Xuanwen Huang
  - Kaiqiao Han
  - Yang Yang
  - admin
  - Quanjin Tao
  - Ziwei Chai
  - Qi Zhu

# Author notes (optional)
# author_notes:
#  - 'Equal contribution'
#  - 'Equal contribution'

date: '2024-01-23T00:00:00Z'
doi: ''

# Schedule page publish date (NOT publication's date).
publishDate: '2023-01-23T00:00:00Z'

# Publication type.
# Accepts a single type but formatted as a YAML list (for Hugo requirements).
# Enter a publication type from the CSL standard.
publication_types: ['paper-conference']

# Publication name and optional abbreviated publication name.
publication: In *ACM TheWebConf 2024 Conference homepage*
publication_short: In *WWW2024*

abstract: Text-attributed Graphs (TAGs), which interlace textual information with graph structures, pose unique challenges and opportunities for joint text and graph modeling. Recently, large language models (LLMs) have greatly advanced the generative and predictive power of text modeling. However, existing research on jointly modeling text and graph structures either incurs high computational costs or offers limited representational power. In this work, we propose GraphAdapter to harness the power of the LLM without fine-tuning its weights on Text-Attributed Graphs. Given a TAG, an adapter GNN is trained to reduce the LLM's error in predicting the next word of text sequences on nodes. Once trained, this GNN adapter can be seamlessly fine-tuned for various downstream tasks. Through extensive node classification experiments across multiple domains, GraphAdapter demonstrates an average improvement of 5% while being more computationally efficient than baselines. We further validate its effectiveness with various language models, including RoBERTa, GPT-2, and Llama 2.

# Summary. An optional shortened abstract.
summary: In this work, we propose GraphAdapter to harness the power of the LLM without fine-tuning its weights on Text-Attributed Graphs. Given a TAG, an adapter GNN is trained to reduce the LLM's error in predicting the next word of text sequences on nodes. 

tags: [Graph Neural Networks, Large Language Model, Text-Attributed Graph]

# Display this page in the Featured widget?
featured: true

# Custom links (uncomment lines below)
# links:
# - name: Custom Link
#   url: http://example.org

url_pdf: 'https://openreview.net/pdf?id=AFJYWMkVCh'
url_code: ''
url_dataset: ''
url_poster: ''
url_project: ''
url_slides: ''
url_source: ''
url_video: ''

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
image:
  caption: 'Framework of GraphAdapter.'
  focal_point: ''
  preview_only: false

# Associated Projects (optional).
#   Associate this publication with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `internal-project` references `content/project/internal-project/index.md`.
#   Otherwise, set `projects: []`.
# projects:
#  - example

# Slides (optional).
#   Associate this publication with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides: "example"` references `content/slides/example/index.md`.
#   Otherwise, set `slides: ""`.
# slides: example
---

