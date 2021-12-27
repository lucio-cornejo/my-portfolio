---
title: "Panelsets in Markdown"
subtitle: ""
excerpt: "Add tabbed sections to your posts."
date: "2021-12-26"
author: "Lucio Cornejo"
draft: false
# layout options: single, single-sidebar
layout: single
categories:
- Theme features
---

## But first, a shortcode trick

Courtesy of panelset.js by Garrick Aden-Buie, from his xaringanExtra package: https://pkg.garrickadenbuie.com/xaringanExtra/#/panelset

For example, this panelset:

{{< panelset class="greetings" >}}
{{< panel name="Hello! :wave:" >}}
  hello
{{< /panel >}}
{{< panel name="Goodbye :dash:" >}}
  goodbye
{{< /panel >}}
{{< /panelset  >}}

## actual code finally?

```{r}
DT::datatable(iris)
```
