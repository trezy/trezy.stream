---
layout: post
title:  "Doing CSS the Trezy way"
# date:   2013-05-06 12:00:00
---

***…which was once called Atomic CSS***

## How do you approach avoiding conflicts in CSS?

Personally, I think that modern scoping approaches are heading in the wrong direction. The cascade is a benefit, rather than something to be shunned. To that end, I prefer to write CSS the same way I would paint a picture. What I mean by that is that I create stylesheets that are *intended* to cascade, built from the ground up.

I start with a reset. Usually Eric Meyer's because it's so small and comprehensive. This gives me a clean, cross-browser canvas on which to build the style of my application.

Next, I style the smallest units we have to work with. Anchors, emphasis, paragraph, header… these elements all receive generic styles that apply across the entire application. This builds a good, consistent design where every link, paragraph, and image looks the same.

Then I start building the larger components and using scoping that way. `header[role=banner]` gets very specific styles because it usually needs to overwrite (or cascade) some of the more generic styles, like anchors and lists.

This approach ensures that my applications are visually consistent, while also avoiding the CSS performance bottlenecks that exist with things like component-scoped styles.

## How do you approach avoiding CSS bloat?

See my previous answer. By building CSS the way I do, it makes the CSS reusable, avoiding the modern issue (*especially* with CSS-in-JS) of writing the same style 3 different times to accommodate 3 different components.

However, deadlines are a thing. When I'm facing a tight deadline, I will create a `shame/` folder and write up a crappy stylesheet with awful styles that are super specific and get the job done. This makes it easy when the time rolls around to deal with tech debt, because you just need to pick a file from the shame folder and go to town.
