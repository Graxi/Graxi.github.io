---
layout: default
title: 'A hack for improving SVG Path hover sensitivity'
categories: [Visualization]
permalink: /visualization/improve-svg-path-hover-sensitivity
comments: true
---

The project management tool, Asana, has a premium feature called *[Timeline](https://asana.com/product/timeline)*. Basically, it helps us to create visualization for the upcoming project. Task bars are connected with each other by arrows. Such user interface is pretty common among visualization tools. Usually, the arrow is drawn using *Bezier curves*.   

![improve-path-hover-sensitivity.jpeg](/assets/2020/20200125.jpeg)

When users hover over a certain curve, the curve as well as the connected tasks will be highlighted. We can simply add `path:hover` in CSS to do the trick. But what if the project is huge and relations between tasks are complicated? We might have to zoom out to see all the tasks. Meanwhile, the curves also become smaller and less obvious. To enhance user experience, it is necessary to improve the curves’ sensitivity to the *hover* event. Even though users may not exactly hover over the tiny path, it still can detect and respond.    

#### Set `pointer-events` to `bounding-box`

A simple and quick fix is to add the attribute `pointer-events` to the `<path>` element and set the value to `bounding-box`. Then the whole`bounding-box` area defined by the `<path>` becomes active to the *hover* event.   

{% include embed-codepen.html pen='2020012501' slug='jOEJYYY' %}

However, when two curves are really close, their `bounding-box` areas might overlap and it is hard to know which curve is on hover.   

{% include embed-codepen.html pen='2020012502' slug='MWYxQwx' %}

#### Wrap each `<path>` with a transparent outline

To solve the problem, I come up with another hack. We can wrap each `<path>` element with a transparent outline which has the same shape but larger `stroke-width`. Even when the curves are close to each other, the solution still works. Please note that in the demo below, the outline color is set to `#eee` instead of `transparent` for better demonstration.   

{% include embed-codepen.html pen='2020012503' slug='dyPrdNN' %}