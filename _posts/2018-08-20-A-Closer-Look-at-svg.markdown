---
layout: default
title: 'A closer look at the use of svg'
categories: [Visualization]
permalink: /visualization/usage-of-svg-on-web
comments: true
---

The way we handle images in the front end is quite different from the way a few years ago when we had to create several versions of the same image and put our little icons on one single sprite image. Nowadays, we are more comfortable using *vector graphics*, replacing *JPEG*, *GIF* with *SVG* formats.

### Web Fonts
Years ago, we were used to sprite images to display icons on the web. Now the regular way of displaying icon images is to create a font file on websites like ***[Fontello](http://fontello.com/)*** with original svg files. I published a ***[post](/automation/2017/07/10/Fontello-SVG-Uploader.html)*** about the tool I created for downloading font files from Fontello. 
Of course we can reference the source svg file in the code but if we have lots of icons, managing these svgs will be troublesome. I would rather see a single web font instead of many svg files or svg code snippets here and there.


### Charts
Almost every front-end web developer has used js libraries like Highcharts to draw various kinds of charts: line charts, pie charts, area charts and so on. Did you notice that the graph rendered by Highcharts is actually a `svg` element? In most cases, we don't care if it is a `svg` element honestly as long as the library can help us to get the work done. However, the information becomes useful when we have to customize the chart a little bit like what I did in a previous post [Create a customized select effect with Highcharts](/visualization/2017/05/15/Customized-Select-Effect.html). Some basic knowlege of SVG `path` element is required in order to do customization based on Highcharts. Please refer to [MDN SVG Tutorials](https://developer.mozilla.org/en-US/docs/Web/SVG/Tutorial/Paths) for further information.

![highcharts-select-effect.gif](/assets/highcharts-select-effect.gif)

### Animated SVG Icons
How do you deal with interactive icons in your code? An interactive icon refers to an icon which will change its state (how it looks like) when you interact with it. For example, a burger icon which signals menu becomes a cross icon upon mouse click. Usually we deal with this icon state change by changing class names of the `i` element. Perhaps we can give a try to [animated SVG icons](https://tympanus.net/Development/AnimatedSVGIcons/) which use javascript to manipulate the `svg` element interactively.

![animated-svg-icon.gif](/assets/animated-svg-icon.gif)

