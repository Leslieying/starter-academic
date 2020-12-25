---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "Use Emacs to Write Markdown"
subtitle: ""
summary: "Emacs as md editor"
authors: [Rui Ying]
tags: [Emacs; Markdown]
categories: [Emacs]
date: 2018-11-25T20:54:20Z
lastmod: 2020-12-25T16:54:18Z
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---
Writing Markdown under emacs can use markdown-mode to perform convenient operations such as syntax highlighting and preview. Specific commands can be obtained through Emacs wiki or documentation.
However, it is worth mentioning that preview should set the markdown command of emacs to a specific variable, for example, "/usr/bin/pandoc" is to connect pandoc and md files, and then Cc Cc P to preview, the preview is on the web So it should be converted to html through pandoc.

Update: now I use Emacs org-mode to export markdown file, and 
use grip-mode to preview it.