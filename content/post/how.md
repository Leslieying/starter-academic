---
title: "How to embed Chinese font in R"
date: 2020-03-31T20:24:01+08:00
draft: false
---

## Aim of this blog

To record the process of embedding Chinese font(or other CJK fonts) in R-created pdf files.

## Used packages

- showtext(primary)
- extrafont

## Example
If you wanna simply show chinese text in plot, showtext package is enought, 'cause it includes a open source font "wqy-microhei"
Here is an example.
``` R
library(showtext)
library(ggplot2)
showtext_auto()

#plot example
set.seed(123)
x <- rnorm(10)
y <- rnorm(10)
df <- data.frame(x=x,y=y)
p <- ggplot(data=df,aes(x,y))+geom_point()+geom_smooth()+
	theme_bw(base_family = "wqy-microhei")
p + xlab("中文")+ylab("字体")
```
## Another Example
If you gonna use other fonts in R, such as Songti("宋体") which is used in many Chinese academic article, you need to firstly download (or copy them from your OS) and import them, and use them as the previous example.
``` R
# import fonts from Windows
library(extrafont)
library(showtext)
library(ggplot2)

#Strategy1 COPY FONTS FROM SYSTEM
#Note: You have to run font_import() again when you have one new font
font_import()
loadfonts(device="pdf")
fonts() #show all fonts

#Straetegy2 ADD ONE FONT
font_add("Songti","~/Downloads/SourceHanSanSerif.otf")

#Strategy3 DOWNLOAD FONTS
font_add_google("Lobster", "lobster")

set.seed(123)
x <- rnorm(10)
y <- rnorm(10)
df <- data.frame(x=x,y=y)
p <- ggplot(data=df,aes(x,y))+geom_point()+geom_smooth()+
	theme_bw(base_family = "Songti")
p + xlab("中文")+ylab("字体")

```
