---
layout: post
title:  "Stop Using ngOptions"
date:   2015-09-02 12:00:00
categories: [javascript]
tags: [angular, javascript]
---

*This article was originally published on 02 September, 2015 at Codepen.io.*

`ngOptions` is awful. It's hard write and even harder to decypher. If you're looking at an `ngOptions` expressions that somebody else wrote? God help you. Luckily, creating select elements in Angular can be so, so much easier. Try this out:

```js
var selectedState, availableStates;

selectedState = '';
availableStates = [
  {
     name: 'Alabama',
     code: 'AL'
  },
  // ...
  {
    name: 'Wisconsin',
    code: 'WI'
  }
];
```

```html
<!-- `ng-model` represents the home for our selected value. -->
<select ng-model="selectedState">
  <!-- This is the default option -->
  <option value="">Select a state</option>

  <!-- The list of states. -->
  <option
    value="{{ state.code }}"
    ng-selected="state.code === selectedState"
    ng-repeat="state in availableStates">
    {{ state.name }}
  </option>
</select>
```

It makes sense — as far as Angular goes — right?

* `option[value]` is what will be set in the model if the option is selected.
* `option[ng-selected]` sets this option as selected if `selectedState` is set to a state code.
* `option[ng-repeat]` loops through the states to create an `option` element for each one.

Now let's look at `ng-options`:

```html
<select
  ng-model="selectedState"
  ng-options="state.name as state.code for state in availableStates">
  <!-- Default selection -->
  <option value="">Select a state</option>
</select>
```

(╯°□°)╯︵ ʎʇıןıqɐuıɐʇuıɐɯ

I'll admit, it's way shorter but even if I wrote them I can't figure out what these things mean when I go back to look at them. Okay, let's break it down anyway. For academic purposes, right?

* `… as …` basically says, "Use `state.name` as a facade for `state.code`." That's kinda cool, as it lets you use an object or an array or a goat or whatever the hell you want for the value and sets the facade as the displayed value. What's not cool is that you'll have to debug what the value actually is if things aren't working the way you'd expect because the value in the markup will be nothing but a single digit. FUUUUUUUUUUUUUU

* `… in …` is your standard looping construct. It's the same thing as `ngRepeat`.

* `thing¹ for thing²` may look familiar if you Coffeescript. This is probably the most confusing part for me, though it's not nearly as bad now that I'm breaking this down. It's just saying do `thing¹` for each `thing²`.

I struggled for a long time trying to figure out how `ngOptions` worked. Then I struggled for a long time trying to figure out how to do it without `ngOptions` because it's impossible to read. Do yourself a favor and follow Occam's Razor.

## On Performance

A coworker pointed out that using `ngOptions` is superior to `ngRepeat` because of it's performance benefits. `ngOptions` creates a single scope which encapsulates all of your options. `ngRepeat` creates a new scope for each `option`. That's true. Creating a new scope for each state - resulting in 50 new scopes - is definitely a performance hit. ~~But if you're using Angular, you obviously don't care about performance anyway. So. There's that.~~ If performance is more important than readability for you, use `ngOptions`, but don't say you haven't been warned.
