---
title: "Creating a table of contents for Xaringan"
subtitle: "Inspired by slidy and reveal.js"
excerpt: "Xaringan is a R package which allows us to create HTML slide presentations using R Markdown and Remark.js ."
date: 2022-05-31
author: "Lucio Cornejo"
draft: false
tags:
- hugo-site
categories:
- rmarkdown
- xaringan
# layout options: single or single-sidebar
layout: single
links:
- icon: door-open
  icon_pack: fas
  name: website
  url: https://toc-for-xaringan-see-slide-2-for-commands.netlify.app/#1
- icon: github
  icon_pack: fab
  name: code
  url: https://github.com/lucio-cornejo/ejemplo-xaringan-TOC
# - icon: newspaper
#   icon_pack: far
#   name: Blog post
#   url: https://education.rstudio.com/blog/2020/07/palmerpenguins-cran/
---

The lack of a table of contents in Xaringan has actually been an open 
[issue](https://github.com/yihui/xaringan/issues/217) since 2019.
Other html presentation formats in R Markdown, such
as **revealjs::revealjs_presentation**  and **slidy_presentation** 
do provide a table of contents, which allows for a faster navigation of the slides.

As Yihui explained in the issue page above, an implementation of a table of contents
for Xaringan requires JavaScript knowledge. Therefore, I've implemented
just that, respecting the properties explained by Yihui in this 
[comment](https://github.com/yihui/xaringan/issues/217#issuecomment-508784341) of his.