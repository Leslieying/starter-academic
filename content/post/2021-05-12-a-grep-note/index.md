---
title: REGEXP note
author: Rui Ying
date: '2021-05-12'
slug: []
categories:
  - Linux
tags: []
subtitle: ''
summary: 'Grep and regexp usage'
authors: []
lastmod: '2021-05-12T18:13:37+01:00'
featured: no
image:
  caption: ''
  focal_point: ''
  preview_only: no
projects: []
---
# Basic syntax

|Character|Description|
|--|--|
| ^ |start
| $ |end
| .| any one character
|* | >1 character
|[]| include
| [^] |not include (e.g. [^A-C] is any one except for ABC)
| \w |word = [A-Za-z0-9]
| \W |inverse of \w

# A useful command
`grep -rnw '/path/to/somewhere/' -e 'pattern'`

- -r recursive
- -n line number
- -w word regexp

# Shortcut

If you use Emacs, you can forget the command and use projectile. This is a project managing package which provides strong search ability with ag/rg (you can still choose grep though).

# Update

In Linux, fuzzy finding fzf is another interesting program.
