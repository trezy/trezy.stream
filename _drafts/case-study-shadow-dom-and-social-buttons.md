---
layout: post
title:  "Case Study: Shadow DOM and Social Buttons"
# date:   2013-05-06 12:00:00
---

Let's face it. We cringe with pain when a client says, "Can we put a Facebook Like button in there?" Social plugins are inherently painful because of the way they have to be loaded in. To get this:

![Facebook like button]()

We have to include the Facebook SDK in our page, plus we have to pump a heavily configured div in where the SDK will inject an iframe to provide encapsulation for the Javascript and CSS that the button includes. Here's an example of the the code they provide:

```html
<!-- Include Facebook's Javascript SDK -->
<div id="fb-root"></div>
<script>(function(d, s, id) {
 var js, fjs = d.getElementsByTagName(s)[0];
 if (d.getElementById(id)) return;
 js = d.createElement(s); js.id = id;
 js.src = "//connect.facebook.net/en_US/sdk.js#xfbml=1&appId=XXXXXXXXXXXXXXX&version=v2.0";
 fjs.parentNode.insertBefore(js, fjs);
}(document, 'script', 'facebook-jssdk'));</script>
<!-- Include a div with configuration options for the SDK to inject its iframe into to -->
<div class="fb-like" data-href="https://developers.facebook.com/docs/plugins/" data-layout="button" data-action="like" data-show-faces="false" data-share="false"></div>
```

Blech. I think there's a better solution.

## Enter Shadow DOM

If you aren't yet familiar with Shadow DOM, you should fix that. [Eric Bedelman](https://www.html5rocks.com/en/profiles/#ericbidelman) has a great series on it on HTML5 Rocks ([Shadow DOM 101](https://www.html5rocks.com/en/tutorials/webcomponents/shadowdom/), [201](https://www.html5rocks.com/en/tutorials/webcomponents/shadowdom-201/), and [301](https://www.html5rocks.com/en/tutorials/webcomponents/shadowdom-301/)). The benefits of Shadow DOM are vast so I'm only going to cover the things that are pertinent for this post, such as encapsulation.

## Why they do what they do

While using these buttons sucks, they're built the way they are for several legitimate reasons. To make sure we're not spinning our wheels let's take a look at why social buttons do what they do.

### The dreaded iframe

There are too many reasons to count for hating the `iframe` element. At this point, however, it sits in the same arena with `table`s. They have been terribly abused and misused in the past but they still have their place in our digital landscape. `table`s *should* be used for tabular data, and `iframe`s *should* be used for a nested browsing context. For example, if I wanted to demo a website I could just link to it **or** I could insert an iframe that then loads that website.
