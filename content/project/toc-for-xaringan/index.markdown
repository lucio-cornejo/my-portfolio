---
title: "A table of contents for Xaringan"
subtitle: "A mixture of Slidy and Reveal.js"
excerpt: "Xaringan is a R package which allows us to create HTML slide presentations using R Markdown and Remark.js ."
date: 2022-05-31
author: "Lucio Cornejo"
draft: false
tags:
- hugo-site
categories:
- xaringan
# layout options: single or single-sidebar
layout: single
links:
- icon: door-open
  icon_pack: fas
  name: website
  url: https://lucio-cornejo.github.io/
- icon: github
  icon_pack: fab
  name: code
  url: https://github.com/lucio-cornejo/my-website
# - icon: newspaper
#   icon_pack: far
#   name: Blog post
#   url: https://education.rstudio.com/blog/2020/07/palmerpenguins-cran/
---

The lack of a table of contents in Xaringan has actually been an open 
[issue] since 2019. Other html presentation formats in R Markdown, such
as **revealjs::revealjs_presentation**  and **slidy_presentation** 
do provide a table of contents, which allows for a faster navigation of the slides.

As Yihui explained in the issue page above, an implementation of a table of contents
for Xaringan is actually a simple project requiring JavaScript. So, I've implemented
just that, respecting the properties explained by Yihui in this 
[comment](https://github.com/yihui/xaringan/issues/217#issuecomment-508784341) of his.