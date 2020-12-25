---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "LSP Mode"
subtitle: ""
summary: " "
authors: [Rui Ying]
tags: [Emacs; LSP]
categories: [Emacs]
date: 2020-12-17T20:42:26Z
lastmod: 2020-12-17T20:42:26Z
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

# What's LSP
LSP is abbreviation of language server protocol, an idea proposed by Microsoft. According to its [website](https://microsoft.github.io/language-server-protocol/), the idea behind the LSP is to standardize the protocol for how such servers and development tools communicate. In short words, LSP expect to standardize common features (i.e. auto-completion, go-to-definition, show-documentation, etc.) among different editors/IDEs. I knew this last night when I was finding some FORTRAN support on emacs; and was surprised by this great idea before I tried it (it was around 1 AM).

# Emacs implementation
There're two packages doint this, LSP-mode and eglot-mode. I tried the former firstly, surpring by its great functions and many integration, but soon found some bugs which I can't solve (e.g. the deprecated function lsp-define-stdio-client error). Naturally I found eglot which is smaller and more suitable for me. I'll show python and fortran suppport as following.

# Python and fortran support
```lisp
(use-package eglot
  :config
  (add-to-list 'eglot-server-programs '((c++-mode c-mode) "clangd")) 
  (add-to-list 'eglot-server-programs '(f90-mode . ("fortls")))
  (add-hook 'python-mode-hook 'eglot-ensure)
  (add-hook 'c-mode-hook 'eglot-ensure)
)
```
The server for python (pyls) and fortran (fortls) respectively need to be pre-installed. Both can be downloaded through pip. Clangd which is used for C and Cpp need to be compiled and installed instead.