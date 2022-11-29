---
title: "Predicting a song's popularity"
excerpt: "Applying Machine Learning to Spotify data, to predict a song's popularity"
date: 2022-07-02
author: "Lucio Cornejo et al."
draft: false
tags:
- hugo-site
categories:
- Machine Learning
- Music
- Python
# layout options: single or single-sidebar
layout: single
links:
- icon: door-open
  icon_pack: fas
  name: website
  url: https://github.com/lucio-cornejo/proyecto-analisis-de-datos-1INF03/blob/main/informes/informe_01.pdf
- icon: github
  icon_pack: fab
  name: code
  url: https://github.com/lucio-cornejo/proyecto-analisis-de-datos-1INF03
---

<p style="margin-bottom: -100px;"> &nbsp; </p>

As part of the course "Data Analysis" from *Pontificia Universidad Católica del Perú*,
a group of students and I applied Machine Learning algorithms, using **Python**,
to uncover which parameters of a song were the best **predictors** for its **popularity**.

We analized a data frame whose rows represented Spotify songs, and whose columns 
contained musical information about the songs, such as tempo, key, time signature, etc,
from which we uncovered, using **logistic regression**, the best song popularity predictors:
**danceability** and **loudness**.