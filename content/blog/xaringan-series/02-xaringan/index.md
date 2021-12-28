---
title: "Issues when reading Xaringan presentations on mobile"
weight: 2
subtitle: "JavaScript to the rescue!"
excerpt: "Grid is the very first CSS module created specifically to solve the layout problems we’ve all been hacking our way around for as long as we’ve been making websites."
date: 2021-12-27
draft: false
---

Perhaps it's just bad luck, but I've encountered a couple of issues on mobile when reading Xaringan slides. \
Here I'll describe how I dealt with those issues, mainly using JavaScript.

## Quickly switch slides

During a mobile Xaringan presentation, if you tap the screen, the next or previous slide will show up. \
However, if you tap many times, and fast, the screen usually activates a zoom. \
Here is a way to disable such screen zoom when double tapping, using `CSS` :

```css
/* Disable double-tap zoom */
html { touch-action: manipulation; } 
```

## Unintended slide change due to tap

In a mobile Xaringan presentation:
- When I've scrolled through a vertically long slide, the tap to activate the scrolling activates an unintended slide change.
- When tapping an image with a link, the slide changes and
    the link is not opened.

The following `JavaScript` code has fixed those problems in my presentations:

```js
// Code to fix the change of slide when 
// scrolling and when clicking some anchors 
let touchmoved;
$('div.remark-slide-container').on('touchend', function(event){
    if(touchmoved === true) {
        // Do not change slide if scrolling took place
        event.preventDefault(); 
        event.stopPropagation();
    } else {
        if(event.target.tagName === "IMG") {
            if (event.target.parentNode.getAttribute("href").includes("https:")) {
                // If there was no scrolling and the user clicked on an image
                // which has an anchor, then do not change slide and open
                // in a ne window the site linked to image touched
                event.preventDefault(); 
                event.stopPropagation();
                window.open(event.target.parentNode.getAttribute("href"));
            } 
        }
    }
}).on('touchmove', function(){
    touchmoved = true; // Scrolling took place
}).on('touchstart', function(){
    touchmoved = false;
});
```

## Swipe to go to previous or next slide, not working

Such functionality is available via `Remark.js`, therefore, it would be expected to work with Xaringan. However, despite it being included in Xaringan presentations I've found online, it hasn't worked for mine.

I've implemented such functionality a little bit different, because my code allows for a _swipe slide change_ to be cancelled
if the user on mobile lifts up his or her finger which induced the tap event, near enough to where the tap initially took place.

The Xaringan presentations I've read on mobile do **not** have 
such _swipe slide change **cancel**_ functionality.

Here is the `JavaScript` code:

```js
// Code to change between slides depending on user screen swipe 
let touchstartX = 0;
let touchendX = 0;
let swiped = false;

function conditional_swipe() {
    // Swiped left
    if (touchendX < touchstartX) {
        if ( (touchstartX - touchendX) > (screen.availWidth)*0.25 ) slideshow.gotoNextSlide();
    } else {
        // Swiped right, because swiped equals true
        if ( (touchendX - touchstartX) > (screen.availWidth)*0.25 ) slideshow.gotoPreviousSlide();
    }
}
    
$('div.remark-slide-container').on('touchstart', event => {
    touchstartX = event.changedTouches[0].screenX;
    swiped = false;
});

$('div.remark-slide-container').on('touchmove', function() { swiped = true; });

$('div.remark-slide-container').on('touchend', event => {
    touchendX = event.changedTouches[0].screenX;
    if (swiped === true) conditional_swipe();
});
```

## Did you know?

Lastly, just a brief mention that many functions related to
the slides in Xaringan (for example, go to previous slide, go to next slide, get the slide's current number, etc) are already defined in **Remark.js**, so you can use them with **JavaScript**. \
In order to see those functions, open a Xaringan presentation on
Desktop, go to the _Console_ (ctrl+shift+i in _Chrome_) and type 
`slideshow.` , then the available functions should pop up.