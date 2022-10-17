---
title: "plyLoadR"
subtitle: "An R alternative to rgl for displaying 3d geometries."
excerpt: "A new widget for mesh evolution visualization."
date: 2022-10-10
author: "Lucio Cornejo"
draft: false
tags:
- hugo-site
categories:
- htmlwidgets
- JavaScript
# layout options: single or single-sidebar
layout: single
links:
- icon: door-open
  icon_pack: fas
  name: website
  url: https://www.youtube.com/watch?v=XbCk_-BOnOc
- icon: github
  icon_pack: fab
  name: code
  url: https://github.com/lucio-cornejo/plyLoadR
---

<p style="margin-bottom: -100px;"> &nbsp; </p>

I was tasked by a researcher from the [Standup project](https://www.standupproject.eu/)
to create an interactive 3D scene where the evolution of meshes was displayed.

My solution consisted of wrapping JavaScript's most complete 3D library, 
**Three.js**, into an R package, in order to implement an htmlwidget
more efficient than rgl (one of R's most popular 3D libraries) for
displaying 3D geometries.
