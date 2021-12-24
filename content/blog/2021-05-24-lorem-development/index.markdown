---
title: "Leaflet library"
subtitle: "originally from JavaScript"
excerpt: "Add tabbed sections with code and results."
date: "2021-12-23"
author: "Lucio Cornejo"
draft: false
# layout options: single, single-sidebar
layout: single-sidebar
categories:
- evergreen
---

<link href="{{< blogdown/postref >}}index_files/panelset/panelset.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/panelset/panelset.js"></script>
<script src="{{< blogdown/postref >}}index_files/htmlwidgets/htmlwidgets.js"></script>
<script src="{{< blogdown/postref >}}index_files/jquery/jquery.min.js"></script>
<link href="{{< blogdown/postref >}}index_files/leaflet/leaflet.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/leaflet/leaflet.js"></script>
<link href="{{< blogdown/postref >}}index_files/leafletfix/leafletfix.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/proj4/proj4.min.js"></script>
<script src="{{< blogdown/postref >}}index_files/Proj4Leaflet/proj4leaflet.js"></script>
<link href="{{< blogdown/postref >}}index_files/rstudio_leaflet/rstudio_leaflet.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/leaflet-binding/leaflet.js"></script>
<link href="{{< blogdown/postref >}}index_files/leaflet-markercluster/MarkerCluster.css" rel="stylesheet" />
<link href="{{< blogdown/postref >}}index_files/leaflet-markercluster/MarkerCluster.Default.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/leaflet-markercluster/leaflet.markercluster.js"></script>
<script src="{{< blogdown/postref >}}index_files/leaflet-markercluster/leaflet.markercluster.freezable.js"></script>
<script src="{{< blogdown/postref >}}index_files/leaflet-markercluster/leaflet.markercluster.layersupport.js"></script>

## Leaflet library

``` r
## Limpieza manual porque janitor me falló

# Información sobre dónde viven los estudiantes
locaciones <- c("la perla,callao","pueblo libre,lima","puno,puno","ventanilla,callao","huancayo, junin","pueblo libre,lima","los olivos, lima","los olivos, lima","los olivos, lima","ventanilla,callao","trujillo,trujillo","san juan de lurigancho,lima","comas,lima","huancayo,junin","miraflores,lima","breña,lima","lima,lima","la victoria,lima","miraflores,lima","san borja,lima","santiago de surco,lima","puno,puno","miraflores,lima","huanuco,huanuco","lima,lima","huancayo,junin","barranco,lima","chorrillos,lima","carabayllo,lima","iquitos,loreto","san jeronimo,cusco","lima,lima","san miguel, lima","independencia,lima","san juan de lurigancho,lima","ica,ica","san isidro,lima","san miguel,lima","breña,lima","lima,lima","el agustino,lima","san miguel,lima","miraflores,lima","wanchaq,cusco","la perla,callao","lima,lima","san borja,lima","comas,lima")
distritos <- unique(c("la perla","pueblo libre","puno","ventanilla","huancayo","pueblo libre","los olivos","los olivos","los olivos","ventanilla","trujillo","san juan de lurigancho","comas","huancayo","miraflores","breña","lima","la victoria","miraflores","san borja","santiago de surco","puno","miraflores","huanuco","lima","huancayo","barranco","chorrillos","carabayllo","iquitos","san jeronimo","lima","san miguel","independencia","san juan de lurigancho","ica","san isidro","san miguel","breña","lima","el agustino","san miguel","miraflores","wanchaq","la perla","lima","san borja","comas"))

# Lista de los distritos, donde después añadiremos su latitud y longitud
coordenadas <- list()
for(i in 1:length(distritos)){
  coordenadas[[i]] <- c(NA,NA) #c(-12.0656,-77.1081) + rnorm(1)
}
names(coordenadas) <- distritos

# Llenamos manualmente las coordenadas de los 27 distritos de la encuesta
coordenadas[[1]] <- c(-12.0656,-77.1081); coordenadas[[2]] <- c(-9.11056,-77.8019)
coordenadas[[3]] <- c(-15.839632,-70.021528); coordenadas[[4]] <- c(-11.855556,-77.073611)
coordenadas[[5]] <- c(-12.0681,-75.2106); coordenadas[[6]] <- c(-11.9917,-77.0706)
coordenadas[[7]] <- c(-8.11167,-79.0286); coordenadas[[8]] <- c(-12.0294,-77.0103)
coordenadas[[9]] <- c(-11.9575,-77.0492); coordenadas[[10]] <- c(-12.1219,-77.0297)
coordenadas[[11]] <- c(-12.0569,-77.0536); coordenadas[[12]] <- c(-12.04318,-77.02824)
coordenadas[[13]] <- c(-12.0653,-77.0311); coordenadas[[14]] <- c(-12.1072,-76.9992)
coordenadas[[15]] <- c(-12.1464,-77.0067); coordenadas[[16]] <- c(-9.92944,-76.2397)
coordenadas[[17]] <- c(-12.1492,-77.0217); coordenadas[[18]] <- c(-12.1692,-77.0244)
coordenadas[[19]] <- c(-11.7961600,-76.9768600); coordenadas[[20]] <- c(-3.75,-73.2444)
coordenadas[[21]] <- c(-13.5447,-71.8839); coordenadas[[22]] <- c(-12.0908,-77.0839)
coordenadas[[23]] <- c(-11.9969,-77.0544); coordenadas[[24]] <- c(-14.0639,-75.7292)
coordenadas[[25]] <- c(-12.0989,-77.0347); coordenadas[[26]] <- c(-12.0483,-76.9833)
coordenadas[[27]] <- c(-13.5253,-71.9658)

# Asignamos la latitud y longitud de los distritos de la encuesta
library(stringr)
latitud  <- c()
longitud <- c()
for(i in 1:length(locaciones)){
  distrito <- str_split(locaciones[i],',')[[1]][1]
  latitud[i]  <- coordenadas[distrito][[1]][1]
  longitud[i] <- coordenadas[distrito][[1]][2]
}

# Mostramos el mapa relevante
library(leaflet)
leaflet(data.frame(lat=latitud,long=longitud)) %>% addTiles() %>% 
        addMarkers(clusterOptions = markerClusterOptions())
```

<div id="htmlwidget-1" style="width:672px;height:480px;" class="leaflet html-widget"></div>
<script type="application/json" data-for="htmlwidget-1">{"x":{"options":{"crs":{"crsClass":"L.CRS.EPSG3857","code":null,"proj4def":null,"projectedBounds":null,"options":{}}},"calls":[{"method":"addTiles","args":["//{s}.tile.openstreetmap.org/{z}/{x}/{y}.png",null,null,{"minZoom":0,"maxZoom":18,"tileSize":256,"subdomains":"abc","errorTileUrl":"","tms":false,"noWrap":false,"zoomOffset":0,"zoomReverse":false,"opacity":1,"zIndex":1,"detectRetina":false,"attribution":"&copy; <a href=\"http://openstreetmap.org\">OpenStreetMap<\/a> contributors, <a href=\"http://creativecommons.org/licenses/by-sa/2.0/\">CC-BY-SA<\/a>"}]},{"method":"addMarkers","args":[[-12.0656,-9.11056,-15.839632,-11.855556,-12.0681,-9.11056,-11.9917,-11.9917,-11.9917,-11.855556,-8.11167,-12.0294,-11.9575,-12.0681,-12.1219,-12.0569,-12.04318,-12.0653,-12.1219,-12.1072,-12.1464,-15.839632,-12.1219,-9.92944,-12.04318,-12.0681,-12.1492,-12.1692,-11.79616,-3.75,-13.5447,-12.04318,-12.0908,-11.9969,-12.0294,-14.0639,-12.0989,-12.0908,-12.0569,-12.04318,-12.0483,-12.0908,-12.1219,-13.5253,-12.0656,-12.04318,-12.1072,-11.9575],[-77.1081,-77.8019,-70.021528,-77.073611,-75.2106,-77.8019,-77.0706,-77.0706,-77.0706,-77.073611,-79.0286,-77.0103,-77.0492,-75.2106,-77.0297,-77.0536,-77.02824,-77.0311,-77.0297,-76.9992,-77.0067,-70.021528,-77.0297,-76.2397,-77.02824,-75.2106,-77.0217,-77.0244,-76.97686,-73.2444,-71.8839,-77.02824,-77.0839,-77.0544,-77.0103,-75.7292,-77.0347,-77.0839,-77.0536,-77.02824,-76.9833,-77.0839,-77.0297,-71.9658,-77.1081,-77.02824,-76.9992,-77.0492],null,null,null,{"interactive":true,"draggable":false,"keyboard":true,"title":"","alt":"","zIndexOffset":0,"opacity":1,"riseOnHover":false,"riseOffset":250},null,null,{"showCoverageOnHover":true,"zoomToBoundsOnClick":true,"spiderfyOnMaxZoom":true,"removeOutsideVisibleBounds":true,"spiderLegPolylineOptions":{"weight":1.5,"color":"#222","opacity":0.5},"freezeAtZoom":false},null,null,{"interactive":false,"permanent":false,"direction":"auto","opacity":1,"offset":[0,0],"textsize":"10px","textOnly":false,"className":"","sticky":true},null]}],"limits":{"lat":[-15.839632,-3.75],"lng":[-79.0286,-70.021528]}},"evals":[],"jsHooks":[]}</script>
