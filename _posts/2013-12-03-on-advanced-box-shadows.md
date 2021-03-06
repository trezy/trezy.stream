---
layout: post
title:  "On Advanced Box Shadows"
date:   2013-12-03 12:00:00
categories: [css]
---

`box-shadow` is arguably one of the coolest things to come out of CSS3. However I've been creating shadows in Adobe Fireworks and Photoshop for years so I feel like I'm too constrained by CSS3's `box-shadow` implementation. In an effort to expand my boxy horizons, I set out on a quest to create some cooler shadows.<!--more-->

**Disclaimer:** At the time of this writing filters and transforms still require browser prefixes to work, though filters will only work in Webkit browsers. I have omitted these prefixes from the code examples here for readability but they will be required if you intend to use these techniques.

## Rocking out with box-shadow

My first attempt at making my shadows more dynamic still uses `box-shadow` but it extends its use to create a new effect. My main goal was to avoid using any extra elements, so all we need is a div and we'll leverage pseudo elements to do the rest of the work.

<p data-height="300" data-theme-id="2296" data-slug-hash="Jrhpc" data-default-tab="css,result" data-user="trezy" data-pen-title="Advanced Box Shadows 1" class="codepen">See the Pen <a href="https://codepen.io/trezy/pen/Jrhpc/">Advanced Box Shadows 1</a> by Trezy (<a href="https://codepen.io/trezy">@trezy</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

What we've done is created two transparent pseudo elements behind our main element. These two pseudo elements then have `box-shadow` applied. This is done so that we can use 2D transforms to angle them, creating a 3D looking `box-shadow` for their parent element.

We also used the `top`, `bottom`, `left`, and `right` properties to keep the shadow from spilling out from the sides of the parent element.

## Box-shadow... without box-shadow?

I was pretty happy with the previous idea, but it didn't look as awesome as I hoped. My next idea was to create the same effect using gradients.

<p data-height="300" data-theme-id="2296" data-slug-hash="aybiL" data-default-tab="css,result" data-user="trezy" data-pen-title="Advanced Box Shadows 2" class="codepen">See the Pen <a href="https://codepen.io/trezy/pen/aybiL/">Advanced Box Shadows 2</a> by Trezy (<a href="https://codepen.io/trezy">@trezy</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

This time we're still using our pseudo elements but instead of giving them `box-shadow`s, we'll give them gradients. We also used a new CSS3 property called `filter`. Make sure to check out all the nifty things it can do [here](http://html5-demos.appspot.com/static/css/filters/index.html). We just use the blur to soften the edges and make it look more like a shadow.

## Oooooh... that's way prettier.

While I was working on this project I ran across a site with an even cooler style of drop-shadow that pointed inward rather than outward:

[Karma](http://http://demo.truethemes.net/Karma-Wordpress/)

All I really had to do was flip my last idea and we were good to go!

<p data-height="300" data-theme-id="2296" data-slug-hash="zEtgJ" data-default-tab="css,result" data-user="trezy" data-pen-title="Advanced Box Shadows 3" class="codepen">See the Pen <a href="https://codepen.io/trezy/pen/zEtgJ/">Advanced Box Shadows 3</a> by Trezy (<a href="https://codepen.io/trezy">@trezy</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

## Conclusion

If you use any of these drop shadows, post a link in the comments! Also, if you come up with any alternative ideas or issues that should be noted, let me know.
