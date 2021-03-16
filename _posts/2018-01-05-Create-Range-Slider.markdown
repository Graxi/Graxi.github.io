---
layout: default
title: 'Lesson learnt from creating a mobile range slider: translate3d vs css left'
categories: [Visualization]
permalink: /visualization/mobile-range-slider-best-practice
comments: true
---

When there are many ways to change an element's position with JavaScript, which one do you prefer? I believe most of you only want to implement the one that brings the best formance. So do I.

In a project about sharing podcasts, a duration range slider needs to be created on the search page. Users can use the duration range slider to filter through all podcasts.

![range-slider.png](/assets/range-slider.png)

Since the project is coded using ReactJS, I had better not use any JQuery plugin but code it with Vanilla JavaScript. In my code, I keep assigning new values(the coordinateX of the cursor) to the pointer's css property `left` on `mousemove` and `touchmove`. The slider works fine on desktop however it becomes laggy on mobile: it always seems to take a while for the pointer to follow up with my cursor. Apparently it has something to do with the animation performance.

Then I started to explore other ways to change an element's position frequently. It works like charm after I use `transform: translate3d(X,0,0)` to set the position of the pointer instead of `left: X`. The sudden improvement of performance amazes me and leads me to the comparison of *[translate3d vs translate vs css left/top vs css margin](https://jsperf.com/translate3d-vs-xy/28)* finally. On that page you can click *Run tests* to see the execution of test cases and find the fastest way.

You may wonder why `translate` and `translate3d` work better than `css left/top` and `css margin`. I will dig into this topic later in another post.

