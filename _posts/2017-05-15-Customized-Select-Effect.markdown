---
layout: default
title: 'Create a customized select effect with Highcharts'
categories: [Visualization]
permalink: /visualization/customize-select-effect-with-highcharts
comments: true
---

We often choose Highcharts as our library when working with charts and data visualization in the front end. Highcharts is a comprehensive library with which you can create various kinds of visual effects. A few days ago, the project manager put up a customized select effect: when you select a part of area on the chart, the background color changes. Since I did not find a quick example on Highcharts website, I decided to create it on my own. You can view the live demo **[HERE](/portfolio/highcharts-highlighted-area.html)**.

Here is my snippet for the customized select effect.
```
  (function highlight(color, strokeWidth) {
    var mainPath = document.getElementsByClassName('highcharts-graph')[0];
    var dValue = mainPath.getAttribute('d').split(' ');
    var container = document.getElementById('container');
    var background = document.getElementsByClassName('highcharts-plot-background')[0];
    var canvasHeight = background.getAttribute('height');
    var offsetLeft = parseInt(background.getAttribute('x')) + 10;
    var defaultStrokeWidth = mainPath.getAttribute('stroke-width');
    var start, end, active;
    container.addEventListener('mousedown', function(e){
    	removeColoredPath();
      start = e.clientX - offsetLeft;
      active = true;
    })
    container.addEventListener('mousemove', function(e){
      if (active) {
        end = e.clientX - offsetLeft;
        calcSubPath(start, end)
      }
    })
    container.addEventListener('mouseup', function(e){
      active = false;
    })
    function calcSubPath (start, end) {
      var array = []
      for (var i = 0; i < dValue.length/3; i++) {
        if (dValue[3*i+1] >= start && dValue[3*i+1]<=end) {
          array.push(dValue[3*i]);
          array.push(dValue[3*i + 1]);
          array.push(dValue[3*i + 2]);
        }
      }
      var firstPoint = array[1];
      var lastPoint = array[array.length - 2];
      if (firstPoint && lastPoint) {
      	array[0] = 'M'
      	var newPath = array.join(' ').concat(' ' + 'L' + ' ' + lastPoint + ' ' + canvasHeight).concat(' ' + 'L' + ' ' + firstPoint + ' ' + canvasHeight)
      	removeColoredPath();
        renderSubPath(newPath);
      }
    }
    function renderSubPath(newPath) {
      var pathElement = document.createElementNS('http://www.w3.org/2000/svg','path');
      pathElement.setAttribute('d', newPath);
      pathElement.setAttribute('stroke', color);
      pathElement.setAttribute('class', 'highcharts-graph colored')
      pathElement.setAttribute('stroke-width', strokeWidth ? strokeWidth.toString() : defaultStrokeWidth);
      pathElement.setAttribute('fill', color || '#384997');
      mainPath.parentElement.append(pathElement);
    }
    function removeColoredPath() {
      var existPath = document.getElementsByClassName('colored')[0];
      if (existPath) {
      	existPath.remove();
      }
    }
  })();
```

