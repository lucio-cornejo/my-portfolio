---
title: "Basic customization"
weight: 1
subtitle: "My preferred modifications to Xaringan presentations"
excerpt: "Grid is the very first CSS module created specifically to solve the layout problems we've all been hacking our way around for as long as w've been making websites."
date: 2021-12-27
draft: false
---
<link href="/rmarkdown-libs/panelset/panelset.css" rel="stylesheet" />
<script src="/rmarkdown-libs/panelset/panelset.js"></script>

<!--#region slide overflow -->
## Slides overflow 

Whenever one of my slides gets too long, it's important to consider if it would be best to continue
typing into a new slide, or simply extend the current one via scrolling capabilities ... after all, 
we are dealing with HTML, not PDF.

In case I need scrolling available for my slides, but I do not want a scrollbar to appear in every slide
of my Xaringan presentation (even if it does not overflow), the following `CSS` code has worked great for me:

```css
/* Fix in case that slides don't automatically admit scrolling whenever there is overflow */
.remark-slide-scaler {
    overflow: auto;
}
```

### First side effect

A common problem on _Desktop_ which arises from dealing with **overflow** that way is that scrolling
through a slide can trigger going to the next or previous slide. \
I deal with that issue using this in the YAML of my Xaringan presentations with scrolling:

```yaml
output: 
    xaringan::moon_reader:
      nature:
        navigation:
          scroll: false
```

### Second side effect

Another issue of adding scrolling capabilities to Xaringan slides is that the region displaying the slide number
does not automatically go to the bottom of the slide whenever scrolling was necessary. \
I've chosen to deal with that drawback via changing the position of the slide counter to the upper right corner of
every slide, like so:

```css
/* Potential fix of slide counter number position when slide overflows */
div[class*="remark-slide-content"] { position: relative; }
div.remark-slide-number {
    top: 0;
    right: 0;
    position: absolute;
    /* Margins to adjust the slide number to almost the exact location where it naturally is */
    /* if we choose to put the slide number on the slide's bottom right corner instead. */
    margin-right: 20px;
    margin-bottom: 12px;
}
```
<!--#endregion-->

<!--#region math overflow -->
## MathJax's overflowing of Math display style equations

Sometimes the overflow can occur horizontally, for example, for long math equations.
I consider best practice to not allow scrolling for math equations unless necessary 
(for example in blog posts where the space for content is quite small). Therefore,
I do not recommend adding scrolling capabilities to math equations in Xaringan ...
simply vertically extend the previously overflowing equation.

Despite this, here is an example of a working scrollable math equation
and how I like to include them in Xaringan:

<style>
    .math-display-style {
    background-color: rgba(150,150,150,0.075);
    padding: 10px 0px 0px 10px; 
    overflow-x: auto;
    -ms-overflow-style: none;  /* Hide scrollbar for IE and Edge */
    scrollbar-width: none;  /*  Hide scrollbar for Firefox */
    }

    /* Hide scrollbar for Chrome, Safari and Opera */
    .math-display-style::-webkit-scrollbar {
    display: none;
    }
</style>

<div class="math-display-style">
  $$
    \text{ The following integral turns out to be related to the main probability distribution in Statistics: }
    \int\limits_{-\infty}^{\infty} e^{-x^2}\, dx = \sqrt\pi \kern1em
  $$
</div>

**Its code:**

```html
<style>
    .math-display-style {
    background-color: rgba(150,150,150,0.075);
    padding: 10px 0px 0px 10px; 
    overflow-x: auto;
    -ms-overflow-style: none;  /* Hide scrollbar for IE and Edge */
    scrollbar-width: none;  /*  Hide scrollbar for Firefox */
    }

    /* Hide scrollbar for Chrome, Safari and Opera */
    .math-display-style::-webkit-scrollbar {
    display: none;
    }
</style>
  
<div class="math-display-style">
  $$
    \text{ The following integral turns out to be related to the main probability distribution in Statistics: }
    \int\limits_{-\infty}^{\infty} e^{-x^2}\, dx = \sqrt\pi \kern1em
  $$
</div>
```
<!--#endregion-->

<!--#region custom panelsets -->
## Custom Xaringan's panelsets

Xaringan's panelsets are great, but I don't like their default styling, particularly because
it can be non trivial to distinguish between tabs. In particular, I've met people who after seeing
the default Xaringan panelset in a slide of mine, they didn't even recognize that they could click on
the tabs to reveal new sections. \
In order to fix that, I prefer styling Xaringan's panelsets this way:



<style>
li.panel-tab {
    border: 1.5px solid black !important;
    background-color: rgb(120, 140, 245) !important;
    background-image: linear-gradient(to bottom, rgba(0,0,0,0), rgba(0,0,0,0.25));
}
</style>

<div class="panelset">
<div class="panel">
<div class="panel-name">blank</div>
<div>

```css
/* Custom Xaringan panelset */
li.panel-tab {
border: 1.5px solid black !important;
background-color: rgb(120, 140, 245) !important;
background-image: linear-gradient(to bottom, rgba(0,0,0,0), rgba(0,0,0,0.25));
}
```


<style type="text/css">
/* Custom Xaringan panelset */
li.panel-tab {
border: 1.5px solid black !important;
background-color: rgb(120, 140, 245) !important;
background-image: linear-gradient(to bottom, rgba(0,0,0,0), rgba(0,0,0,0.25));
}
</style>
</div>
</div>
<div class="panel">
<div class="panel-name">blank</div>
<div>

```js
let panels_names;
document.addEventListener('DOMContentLoaded', function() {
  panels_names = document.querySelectorAll('li.panel-tab a');
  panels_names[0].innerHTML="CSS of this panels";
  panels_names[1].innerHTML="JavaScript code to fix the panelset in this page"
  panels_names[0].click();
});
```
</div>
</div>
</div>

For some reason, the usual way to create Xaringan's panelsets \
(`## some header {.panelset}`) \
does not work for me in this page, and neither did the workarounds
mentioned [here](https://joys.solarchemist.se/blog/seedling/) and
[here](https://gist.github.com/gadenbuie/fa7b75e5447ea52d5d1f13d2f15ca7fa).

Here is the R Markdown code for how I applied the previous Xaringan panelset, but I've removed the pair of three backticks of both chunks (they are included in the actual panelset's R Markdown code) because the following text
would not display correctly unless I removed them :

```text
<div class="panelset">
<div class="panel">
<div class="panel-name">blank</div>
<div>
{css, echo=TRUE}
/* Custom Xaringan panelset */
li.panel-tab {
border: 1.5px solid black !important;
background-color: rgb(120, 140, 245) !important;
background-image: linear-gradient(to bottom, rgba(0,0,0,0), rgba(0,0,0,0.25));
}
</div>
</div>
<div class="panel">
<div class="panel-name">blank</div>
<div>
{js, eval=FALSE, echo=TRUE}
let panels_names;
document.addEventListener('DOMContentLoaded', function() {
  panels_names = document.querySelectorAll('li.panel-tab a');
  panels_names[0].innerHTML="CSS of this panels";
  panels_names[1].innerHTML="JavaScript code to fix the panelset in this page"
  panels_names[0].click();
});
</div>
</div>
</div>
```

<script>
  let panels_names;
  document.addEventListener('DOMContentLoaded', function() {
    panels_names = document.querySelectorAll('li.panel-tab a');
    panels_names[0].innerHTML="CSS of this panels";
    panels_names[1].innerHTML="JavaScript code to fix the panelset in this page"
    panels_names[0].click();
  });
</script>
<!--#endregion-->
