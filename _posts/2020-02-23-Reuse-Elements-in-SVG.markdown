---
layout: default
title: 'Making elements reusable in SVG'
categories: [Visualization]
permalink: /visualization/making-elements-reusable-in-svg
comments: true
---

In a data visualization project, there may be similar elements with tiny differences, which can be seen as one element receiving different parameters. In the previous post *[A hack for improving SVG Path hover sensitivity](https://subtleworks.cn/visualization/improve-svg-path-hover-sensitivity)*, I gave an example of creating a wider transparent outline for each path.   

{% include embed-codepen.html pen='2020012503' slug='dyPrdNN' %}

When creating the inner and outer path, I managed to reuse the elements predefined in `<defs>` with `<use>` tag. Now let me show you how it works step by step with a simple example.   

#### Reuse elements with `<use>` tag

SVG provides `<use>` tag to reuse elements. In the example below, there are two lines. The one above is the original element and the one below is cloned with `<use>`. The only difference is the coordinate in Y axis.   

{% include embed-codepen.html pen='2020022301' slug='mdJOLLj' %}

There are two problems with `<use>` tag:
- You can only clone an element but not modify the attributes of the original element.
- The values of x and y attributes are set relatively based on the coordinates of the original element. It means we need to know in advance its position.

#### Define reusable elements with `<defs>` tag

The two problems above can be solved if we also import `<defs>` tag. Elements predefined in `<defs>` will not be displayed. In addition, when we reuse them, we can not only add or modify the attributes of original ones such as `stroke` and `stroke-width` but also set absolute coordinates for them.   

It should be noted that the absolute coordinates, or the values of `x` and `y` attributes of `<use>`, becomes the origin of coordinates for the newly duplicated element.   

{% include embed-codepen.html pen='2020022302' slug='ExjNGRZ' %}

