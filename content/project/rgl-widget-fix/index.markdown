---
title: "Fixing the rgl package for mobile"
subtitle: "Combining R and JavaScript"
excerpt: "The rgl package is a great tool for creating graphics in the browser, but their interactivity only works well in desktop."
date: 2022-01-27
author: "Lucio Cornejo"
draft: false
tags:
- hugo-site
categories:
- rmarkdown
- frontend
layout: single
links:
- icon: door-open
  icon_pack: fas
  name: website
  url: https://rgl-graphic-mobile-fix.netlify.app/
- icon: github
  icon_pack: fab
  name: code
  url: https://github.com/lucio-cornejo/fix-rgl-for-mobile
---

The `rgl` package provides R another way of creating interactive 
graphics for the broswer. However, such interactivity only
completely works for desktop. Therefore, `rgl` graphics could
not be rotated when interacted via a tablet or mobile, which
was the necessary case for the doctoral project of my 
future thesis advisor.

In this project, I implement a solution via JavaScript in order
to replicate, for non desktop users, the rotation of the graphics
provided by the `rgl` package.