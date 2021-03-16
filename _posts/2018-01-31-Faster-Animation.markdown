---
layout: default
title: 'Faster animation with GPU accelerated CSS'
categories: [Visualization]
permalink: /visualization/animation-with-GPU-accelerated-css
comments: true
---


> *Lift not the painted veil which those who live*
> *Call Life: though unreal shapes be pictured there,*
> *And it but mimic all we would believe*

Last time I shared my experience of creating a mobile range slider in *[Lesson learnt from creating a mobile range slider: translate3d vs css left](/visualization/2018/01/05/Create-Range-Slider.html)* and promised that I would discuss further the topic of faster animation.

I have been involved in a few projects focused on css/js animation and encountered performance problems of the animation sometimes. What I used to do is to find a quick fix like `transform: translateZ(0)` on the Internet and see if it works. It does work in most cases. But why? Is that anything in common among these magical fixes?

I researched for a while and also read a few articles on browser rendering before I heard concepts like **GPU accelerated CSS**. 
After reading one *[article](https://www.chromium.org/developers/design-documents/gpu-accelerated-compositing-in-chrome)*, I get some basic understanding of the painting process in a browser and come to know a layer can have its own compositing layer which will be accelerated by GPU if
* it is used by a `<canvas>` element
* it uses a CSS animation for its opacity or uses an animated webkit transform
* it uses accelerated CSS filters

![GPU-compositing-in-Chrome.png](/assets/GPU-compositing-in-Chrome.png)


Therefore, I have **summarized a few tips for you to improve animation performance**:
* Use CSS property `will-change` on elements that will be animated but don't overuse it
* Use `transform: translate3d(x,y,z)` to update the position of elements via CSS
* Use `window.requestAnimationFrame()` instead of `window.setInterval()`
* To better understand the painting work triggered by CSS properties, check it on *[csstriggers](https://csstriggers.com/)*
* Explore situations to change a layer into **compositing layer** when the performance is not good


