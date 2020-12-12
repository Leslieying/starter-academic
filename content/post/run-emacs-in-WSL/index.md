---
title: "Run Emacs in WSL"
subtitle: ""
summary: ""
authors: [Rui Ying]
tags: [Emacs; WSL]
categories: [Emacs]
date: 2020-12-12T14:39:42Z
lastmod: 2020-12-12T14:39:42Z
featured: false
draft: false
---
# Emacs in Windows
Following are multiple ways to run emacs in Windows.
- Emacs for windows
- WSYS2 (pacman -S Emacs)
- WSL emacs

The first one should be the easiest way to install and run, yet it's not so good to use. For example, I'm struggling with environmental variable. Firstly, There're `C:\Users\usrname\app\roaming` and `C:\Users\usrname`  comfusing me which one should be `$HOME`, especially when I use university-distributed pc and don't have root permission to modify System variable. Secondly and similarly, when I use python, which python should I use, anaconda? The .exe file from python website? or the automatic answer, python in the windows store? The third one, I can't use `tramp-mode` easily as in other OS. The last one, when I open emacs by pressing their shortcut, the default path through entring `C-x C-f` is not `~` that I want. Certainly you can define an exact path in the property, but emmm, it's just so hard to use.

WSYS2 is good to use as well, they provide unix-like environment and you can use `pacman` like in arch-linux. But I met an issue that I can't download package after downloading python-pip, which means I can't use python like in unix (I don't know why either).

Finally, we have the last option: downloading Debian/CentOS in windows store and use X-server (e.g. MobaXterm, VcXsrv) to visualise GUI instead of runing in WSL terminal (add `"echo export DISPLAY=0:0"` in `/etc/profile`). Honestly, I didn't find it significantly faster than in WSYS2, but I can use it very conveniently. Of course, "relatively complex" things always exist. For instance I need to install emacs 27.1 by compling source codes, because in the apt the dafult emacs version is 26.1. Also, if you use high DPI screen as me, you need to open compatibility and change DPI setting in shortcut property. Lastly, the CJK font and input method for emacs seems to be another brain-blowing thing...

There're also other alternative ways including
- Docker
- WSL2
But I didn't try them, and don't want to yet.