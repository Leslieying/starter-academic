---
title: Try Windows Terminal + Powershell
author: Rui Ying
date: '2021-07-12'
summary: 'A nice Windows programming environment in 2021'
slug: []
categories:
  - Emacs
  - Linux
tags: []
---

The new [Windows Terminal](https://github.com/microsoft/terminal) seems to make programming on Windows much better than ever. It is now beautiful, customizable as its counterparts. Today I just found it included a new GUI setting to make self-customization easier and more friendly.

# Download/Upgrade

Find latest Windows Terminal and Powershell in their release pages ([windows terminal](https://github.com/microsoft/terminal/releases), [powershell](https://github.com/PowerShell/PowerShell/releases))


# Customization

The latest windows terminal includes a GUI setting interface (the original one is simply a json file), to open it just `Ctrl + ,` and play with your own!

It is also possible to do something as below to enable Emacs keybinding and set new theme

``` sh
# install posh-git and oh-my-posh
Install-Module -Name posh-git -AllowPrerelease -Force

Install-Module oh-my-posh -Scope CurrentUser -RequiredVersion 2.0.412

# install PSreadline to enable Emacs keybinding
Install-Module -Name PSReadLine -Scope CurrentUser -Force -SkipPublisherCheck

# edit profile file
sublime_text.ext $PROFILE
# then add
Import-Module posh-git
Import-Module oh-my-posh
Set-Theme pure

# if you use Emacs keybinding
Set-PSReadLineOption -EditMode Emacs
```
Couple with [the other new post](https://www.ruiying.online/post/2021-07-12-use-emacs-on-a-remote-shell/), Now I can operate remote file more smoothly.
