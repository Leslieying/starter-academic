---
title: Install and use Emacs 28 Native comp (gccemacs)
author: Rui Ying
date: '2021-07-02'
slug: []
categories:
  - Emacs
tags:
  - Emacs; WSL
subtitle: ''
summary: ''
authors: []
lastmod: '2021-07-02T19:25:48+01:00'
featured: no
image:
  caption: ''
  focal_point: ''
  preview_only: no
projects: []
---

# Features

[GCC Emacs](http://akrl.sdf.org/gccemacs.html) uses libgccjit to compile and run Emacs Lisp as native code in form of re-loadable elf files. Therefore, it reaches a 3.8 times faster performance.

More details can be found in the [paper](https://zenodo.org/record/3736363).

# Installation

## MacOS

First enable gcc with libgccjit. `cd /usr/local/Homebrew/Library/Taps/homebrew/homebrew-core/Formula` and edit `gcc.rb`

``` diff
-    languages = %w[c c++ objc obj-c++ fortran]
+    languages = %w[c c++ objc obj-c++ fortran jit]

    args = %W[
      --prefix=#{prefix}
      --libdir=#{lib}/gcc/#{version_suffix}
      --disable-nls
      --enable-checking=release
      --enable-languages=#{languages.join(",")}
      --program-suffix=-#{version_suffix}
      --with-gmp=#{Formula["gmp"].opt_prefix}
      --with-mpfr=#{Formula["mpfr"].opt_prefix}
      --with-mpc=#{Formula["libmpc"].opt_prefix}
      --with-isl=#{Formula["isl"].opt_prefix}
      --with-zstd=#{Formula["zstd"].opt_prefix}
      --with-pkgversion=#{pkgversion}
      --with-bugurl=#{tap.issues_url}
+     --enable-host-shared
    ]
```

Then there are (at least) three ways to compile Emacs native comp (emacs-plus@28 works for my laptop with Big Sur 11.4).

- https://github.com/d12frosted/homebrew-emacs-plus.git
- https://github.com/daviderestivo/homebrew-emacs-head
- https://github.com/jimeh/build-emacs-for-macos.git

After compilation, it takes a while to compile your lisp codes. Just wait.

## Windows

### Enable WSL2 and install ArchWSL

To enable WSL2 in Windows, follow the steps in [microsoft doc](https://docs.microsoft.com/en-us/windows/wsl/install-win10). You can also download kernel [update package](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi) if you have already installed it.

Since Arch Linux is not included in the Microsoft Store, we need to install it manually. However, yuk7 has a project to make this possible and easy to do based on a perfect [documentation](https://wsldl-pg.github.io/ArchW-docs/How-to-Setup/).

``` sh
#set root password
passwd

#setup sudoers
echo "%wheel ALL=(ALL) ALL" > /etc/sudoers.d/wheel

#add user
useradd -m -G wheel -s /bin/bash {username}

#set user password
passwd {username}

#exit and use shell under windows to set default user
.\Arch.exe config --default-user {username}

#login again to Arch
sudo pacman-key --init
sudo pacman-key --populate

#update system
pacman -Syu

#install package as you want
pacman -S <package>
```

### Install yay (an AUR helper)

``` sh
pacman -S --needed git base-devel
git clone https://aur.archlinux.org/yay.git
cd yay
makepkg -si
```

### Add gpg key of libgccjit

This step is needed because libgccjit key is not included in archwsl. Use the command below to add it.

``` sh
#replace <key> with the hashed keys according to cmd notification
gpg --keyserver keyserver.ubuntu.com --recv-key <key1> <key2>
```

### Install Emacs 28 (each one should work)

``` sh
yay -S emacs-gcc-wayland-devel-bin
yay -S emacs-native-comp-git-enhanced
yay -S emacs-native-comp-git

#from source code
git clone https://aur.archlinux.org/emacs-native-comp-git.git
cd emacs-native-comp-git
makepkg --syncdeps --install
```
### Use XServer to run GUI app

After installation, you can run Emacs but it won't show xwindow as you expect. You need use a XServer (e.g., MobaXterm, X410, VcXsrv) to do this. Several months ago I've written a post that describes my experience of using Emacs on Windows, [check it](https://www.ruiying.online/post/run-emacs-in-wsl/) if you like.

```
#add this line to your .zshrc/.bashrc
export DISPLAY=$(cat /etc/resolv.conf | grep nameserver | awk '{print $2; exit;}'):0.0

#test if works, expected output: <IP:port>
echo $DISPLAY

#or
nc -v <IP> 6000
```


# Emacs configurations

### Clone straight.el (optional)

The original boostrap code of straight.el won't work in WSL2, so we need clone the repository to the `.emacs.d` directory. See the Debugging section of doc.

```
git clone https://github.com/raxod502/straight.el.git ~/.emacs.d/straight/repos/straight.el
```

### Native comp support 

Download your configuration file with codes below to unleash its power.

``` lisp
(when (and (fboundp 'native-comp-available-p)
           (native-comp-available-p))
  (progn
    (setq native-comp-async-report-warnings-errors nil)
    (setq comp-deferred-compilation t)
    (add-to-list 'native-comp-eln-load-path (expand-file-name "eln-cache/" user-emacs-directory))
    (setq package-native-compile t)
    ))
```

## Conclusion

My experience is that it's significantly faster on Mac, which is why I spend more time cloning this on Windows. However, on WSL2 I really can't find the difference because the Emacs 28 without native comp feature on WSL2 is already very fast (init time < 1.0s). Given the blurry problem of running GUI app based on XServer on a high DPI screen, consider twice before your decision.
