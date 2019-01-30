---
layout: post
title:  "On Handlebars and Template Tags"
date:   2014-06-17 12:00:00
categories: [javascript]
tags: [handlebars, javascript]
---

[Handlebars](http://handlebarsjs.com) is *awesome*. I can separate my template logic from my application logic? Yes, please. When I try to use Handlebars in my local editor, though, it vomits all over those ugly `<script>` tags. Fortunately there's an awesome, future-friendly, spec-compliant solution - the `<template>` tag.

`<template>` tags are super cool in a lot of ways. From the [HTML5 Rocks article](http://www.html5rocks.com/en/tutorials/webcomponents/template/), here are the pillars of `<template>` tags:

1. Its content is effectively inert until activated. Essentially, your markup is hidden DOM and does not render.
1. Any content within a template won't have side effects. Script doesn't run, images don't load, audio doesn't play... until the template is used.
1. Content is considered not to be in the document. Using `document.getElementById()` or `querySelector()` in the main page won't return child nodes of a template.
1. Templates can be placed anywhere inside of `<head>`, `<body>`, or `<frameset>` and can contain any type of content which is allowed in those elements. Note that "anywhere" means that `<template>` can safely be used in places that the HTML parser disallows...all but content model children. It can also be placed as a child of `<table>` or `<select>`:

``` html
<table>
  <tr>
    <template id="cells-to-repeat">
      <td></td>
    </template>
  </tr>
</table>
```

## Why isn't this being used elsewhere?

That's a great question. I can only speculate but I'd reckon it has something to do with the recency / lack of support. `<template>` is supported in most browsers, though [Can I Use](http://caniuse.com/#search=template) tells us that we're lacking support in Internet Explorer (big surprise), Safari 7, and Blackberry. Luckily, we can add [this shim](http://jsfiddle.net/brianblakely/h3EmY/) if we need to make it work everywhere. You can read more about the `<template>` tag and how to use it in [this tutorial on HTML5 Rocks](http://www.html5rocks.com/en/tutorials/webcomponents/template/).

Here's the coolest thing, though - current Handlebars users will actually have to write *less* code. Check it:

{% raw %}
``` html
<!-- Handlebars recommended template block syntax -->
<script type="text/x-handlebars-template" id="article-template">
  <article>
    <h1>{{title}}</h1>

    {{content}}
  </article>
</script>
```
{% endraw %}

...just swap the `<script>` tags for `<template>` tags:

{% raw %}
``` html
<!-- The exact same thing using template tags -->
<template id="articleTemplate">
  <article>
    <h1>{{title}}</h1>

    {{content}}
  </article>
</template>
```
{% endraw %}

And blammo, you're using awesome new HTML5 tech. Your editor and I will love you for it. 😉

## The catch

As [@joao](http://codepen.io/joao/) points out in the comments on Codepen, there's always gotta be *something* wrong. Take a look at this code:

{% raw %}
``` html
<template id="tableTemplate">
  <table>
    {{#each}}
    <tr>
      <td>{{content}}</td>
    </tr>
    {{/each}}
  </table>
</template>
```
{% endraw %}

Looks legit, right? Unfortunately it breaks in the browser. The parser still requires the code inside the `<template>` tag to be valid HTML which means you can't have any content in a table unless it's also inside a cell (`<td>`). You can, however, create your table cells / rows in a template tag and use them in a table:

{% raw %}
``` html
<table></table>

<template id="tableTemplate">
  {{#each}}
  <tr>
    <td>{{content}}</td>
  </tr>
  {{/each}}
</template>
```
{% endraw %}

It's not ideal and I would definitely prefer a better DOM API for it. Still, this stuff is super cool and I'll be using it all over the place. If you take advantage of it, let me know! I'll leave you with my implementation of `<template>` tags and Handlebars:

<p data-height="300" data-theme-id="2296" data-slug-hash="yxqCJ" data-default-tab="js,result" data-user="trezy" data-pen-title="Using template tags with Handlebars" class="codepen">See the Pen <a href="https://codepen.io/trezy/pen/yxqCJ/">Using template tags with Handlebars</a> by Trezy (<a href="https://codepen.io/trezy">@trezy</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>
