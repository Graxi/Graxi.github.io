---
layout: default
title: 'Draw a star-shaped chart with Canvas (2): Paint colors'
categories: [Visualization]
permalink: /visualization/draw-star-shaped-chart-with-canvas-2
comments: true
---

This is the second post on the topic of *Draw a star-shaped chart with Canvas*. This time I will cover how to paint different colors on the chart. You can visit the online demo **[HERE](/portfolio/star-shape-chart.html)**.

### Paint Colors
This chart is designed to visualize the number of followers of a track from different social media platforms. Each social media platform has a unique color. For example, the track has **2553** followers in total with **25%** from **Facbook**, **25%** from **Twitter**, **15%** from **Instagram** and **35%** from **Youtube**. The colors for these four platforms are **#003840**, **#005A5B**, **#007369** and **#008C72** respectively. So the next step is to paint colors on the chart proportionally.

With some basic knowledge of `canvas`, we know it is pretty easy to fill a rectangle or a circle. Here it seems we should paint a circle except that the area outside the star shape chart is not colored at all. This may remind you of the usage of `canvas clip`.

As [MDN](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial/Compositing) defines *Clipping paths* as:
> A clipping path is like a normal canvas shape but it acts as a mask to hide unwanted parts of shapes...Everything that falls outside of this path won't get drawn on the canvas...You use `clip()` instead of `closePath()` to close a path and turn it into a clipping path instead of stroking or filling the path.

The idea is to draw a star shape outline first, clip the outline path and paint the circle that wraps the star shape. To paint a circle, we need to make use of the `arc()` method. Please note here **we should fill a fan-shaped area instead of an arc**. That's why we should move to the center point before we draw an arc each time. Here is the complete version of the js snippet.
```
	var canvas = document.getElementById('canvas');
	var canvasWidth = canvas.width;
	var canvasHeight = canvas.height;
	var ctx = canvas.getContext('2d');

	var R = 90
	var r = 78;
	ctx.beginPath();
	ctx.moveTo(1/2 * canvasWidth, 1/2 * canvasHeight - r);
	for(var i = 1; i <= 28; i++) {
	  if (i%2 == 1) {
	    ctx.lineTo(1/2 * canvasWidth + Math.sin(1/14*Math.PI*i)*R, 1/2 * canvasHeight - Math.cos(1/14*Math.PI*i)*R)
	  } else {
	    ctx.lineTo(1/2 * canvasWidth + Math.sin(1/14*Math.PI*i)*r, 1/2 * canvasHeight - Math.cos(1/14*Math.PI*i)*r)
	  }
	}
	ctx.lineWidth = '2';
	ctx.strokeStyle = '#fff';
	ctx.stroke();
	ctx.clip();
	
	var data = [
	  {name: 'Facebook', ratio: 0.25, color: '#003840'},
	  {name: 'Twitter', ratio: 0.25, color: '#005A5B'},
	  {name: 'Instagram', ratio: 0.15, color: '#007369'},
	  {name: 'Youtube', ratio: 0.35, color: '#008C72'}
	]

	var startPoint = 0;
	data.forEach(function(ele){
	  ctx.beginPath();
	  ctx.moveTo(1/2 * canvasWidth,1/2 * canvasHeight);
	  ctx.arc(1/2 * canvasWidth,1/2 * canvasHeight,R,startPoint, startPoint + ele.ratio * 2 * Math.PI);
	  ctx.fillStyle = ele.color;
	  ctx.fill();
	  startPoint += ele.ratio * 2 * Math.PI;
	})
	
	ctx.beginPath();
	ctx.arc(1/2 * canvasWidth, 1/2 * canvasHeight, 70, 0, 2 * Math.PI);
	ctx.fillStyle='#fff';
	ctx.fill();
	ctx.stroke();
	ctx.closePath();
```


	


