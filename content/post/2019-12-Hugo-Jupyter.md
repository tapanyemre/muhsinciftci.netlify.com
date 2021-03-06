---
title: 'Publishing Jupyter Notebooks with Hugo'
subtitle: 
summary:
authors:
- admin
tags:
- Hugo, Jupyter
categories: []
date: "2019-12-07T00:00:00Z"
lastmod: "2019-12-07T00:00:00Z"
featured: featured.jpg
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Placement options: 1 = Full column width, 2 = Out-set, 3 = Screen-width
# Focal point options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
image:
  placement: 2
  caption:
  focal_point: Top
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---

The Jupyter notebooks and Hugo websites by themselves are perfect but when it comes to publishing Jupyter Notebooks with Hugo we face some problems, since Hugo directly works with markdown files. The easiest way to handle this problem is first to create a Gist on github. Then, we embed the Gist code to the Markdown file. Then resulting output is pretty much the same as the original Jupyter Notebook. Otherwise we have to manually work on the .md file and this can be quite exhausting!

<script src="https://gist.github.com/muhsinciftci/beac12e51a4f7e9a5dc8ac1f730353b5.js"></script>





