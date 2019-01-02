---
layout: post
title:  "Let's Play: CSS"
# date:   2013-05-06 12:00:00
---

You may not know this, but it's been brought to my attention that CSS is hard. Reflecting on the years I've spent perfecting my Stylesheet Fu, I suppose that's true. CSS is full of inconsistent syntax, strange relationships, and ugly hacks. The preprocessor world? It's not much better. So let's do this - we're going to lift the hood on CSS and try to cover everything that isn't often covered.

## The DOM

[The DOM](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model) is a map of how all of the elements in a page relate to each other. In CSS it determines how we build our selectors to traverse the page.

## The Box Model

The CSS Box Model is a demonstration of the way an elements height and width, padding, margin, and border interact with each other to create the elements final size.

<figure class="pull-left">
  <img src="https://trezy.sh/1JUvCt.png" alt="">

  <figcaption>The CSS Box Model via <a href="//developer.mozilla.org/en-US/docs/Web/CSS/CSS_Box_Model/Introduction_to_the_CSS_box_model">Mozilla Developer Network</a></figcaption>
</figure>

There's a pretty nasty issue with the box model, however. Without changing anything in your stylesheets the actual width of an element will be the sum the element's `width`, `padding`, and `border-width` properties. Luckily there's a snazzy property called `box-sizing` that can fix the issue for us. Setting `box-sizing: border-box` on an element will fix its box model. We'll talk more about utilizing this in a later article.
