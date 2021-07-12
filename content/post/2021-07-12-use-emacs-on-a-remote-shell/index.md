---
title: Use Emacs on a remote shell
author: Rui Ying
date: '2021-07-12'
slug: []
categories:
  - Emacs
tags: []
subtitle: ''
summary: 'Another way to run Emacs'
authors: []
lastmod: '2021-07-12T22:01:02+01:00'
featured: no
image:
  caption: ''
  focal_point: ''
  preview_only: no
projects: []
---

My daily work includes edit files remotely via `ssh`. Thus I have some [solutions](https://www.ruiying.online/post/run-emacs-in-wsl/) to run Emacs on Windows and use `tramp` to make this possible without costing time learning a new editor. However, `tramp` would be relatively slow if I'm using `scp` protocol. So I decided to try to directly run Emacs on remote terminal.

# Install latest Emacs

I can't and won't wish to install Emacs 26/27/28 via compiling in a CentOS machine without root permission. Thus my way is to use conda to run it.

```sh
conda install Emacs -c conda-forge
```

# Enable mouse operation for terminal Emacs

```lisp
(unless (display-graphic-p)
  (xterm-mouse-mode 1)
  (global-set-key (kbd "<mouse-4>") 'scroll-down-line)
  (global-set-key (kbd "<mouse-5>") 'scroll-up-line)
  )
```

# Use new Emacs without activating conda

However, I've got a new task that if I add miniconda to the top of `$PATH`, my model which uses python2 won't work properly. So I alias Emacs directly to `~/miniconda/bin/emacs-27.2` to avoid using default last-century (actually not) Emacs. And if I add a package `conda.el` to manage conda environment in shell:

```lisp
(use-package conda
  :config
  (setq conda-anaconda-home (expand-file-name "~/miniconda3"))
  (setq conda-env-home-directory (expand-file-name "~/miniconda3"))
  (conda-env-initialize-interactive-shells))
```

I just found I can simply put conda path before default Emacs but after python2. But the ad of my way is that I can use conda packages like pylsp without exporting its path in the shell profile.

# The last interesting thing

I just update some conda packages and found Emacs broken because of some dependencies. After googling I surprisingly found conda can rollback, how amazing!

```sh
conda list --revisions
conda install --revision [revision number]
```
