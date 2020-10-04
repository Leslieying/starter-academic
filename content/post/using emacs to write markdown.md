---
title: Emacs下写markdown
date: 2018-11-25 20:54:42
summary: ""
draft: false
---

在emacs下编写Markdown可以通过package markdown-mode来进行语法高亮以及preview等等方便的操作。具体的命令可以通过Emacs wiki或者documentation来获得。  
不过值得一提的是，preview要将emacs的markdown command设置为一个具体的变量，例如"/usr/bin/pandoc"就是将pandoc和md文件连接起来，然后C-c C-c P来预览，预览是在web中实现，所以应该是将md文件通过pandoc转为了html。
