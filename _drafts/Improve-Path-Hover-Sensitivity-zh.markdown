---
layout: post
title: '对SVG Path实现模糊focus的小技巧'
categories: [Visualization]
permalink: /visualization/improve-svg-path-hover-sensitivity
---

项目管理工具Asana有一个付费功能叫Timeline，简单来说它可以帮我们为接下来的项目任务安排创建一个可视化视图。任务框之间用箭头连接，表示它们之间的关联。这样的界面设计在其他可视化工具里也很常见，通常，箭头的部分是由SVG的贝兹曲线来实现。  

![improve-path-hover-sensitivity.jpeg](/assets/2020/20200125.jpeg)

当用户的鼠标hover在某段曲线时，这段曲线及其连接的两个相关任务将会被高亮显示。在项目任务数量少的情况下，在CSS文件中使用`path:hover`就能实现想要的效果。但假设项目十分庞大，任务之间关系相当复杂，用户往往需要先缩小视图才能看到全部任务，此时任务框和中间连接的曲线在视觉上也变得越来越不明显。为了提升用户体验，需要提高曲线对于hover事件的敏感度，即使鼠标距离连线还有一点距离，也能够及时感知并高亮显示。  

#### 将`pointer-events`属性值设置为`bounding-box`

一个简单的方法是给表示曲线的`<path>`元素添加`pointer-events`属性，并将值设置为`bounding-box`。这样一来，只要鼠标停留在包含曲线的**矩形框**范围内，`<path>`元素便能响应hover事件。  

{% include embed-codepen.html pen='2020012501' slug='jOEJYYY' %}

但这种做法的弊端是：当两条曲线很接近时，它们的`bounding-box`会有重合的可能，于是就无法准确得知用户具体hover在哪条曲线上。  

{% include embed-codepen.html pen='2020012502' slug='MWYxQwx' %}

所以这种简单快捷的方法只适合于曲线并不密集的情形。

#### 为每一条曲线添加一层更宽的透明外廓

为了实现这个功能，有一个笨拙的替代方法：为每个曲线元素添加一个路径相同但更宽的透明外廓。这样既不会影响界面显示，同时也能提高曲线对于hover事件的敏感度，并且足以应付曲线密集的复杂情形。为了避免重复创建相同的`<path>`元素，在代码中我使用了`<use>`元素，具体实现如下。  

{% include embed-codepen.html pen='2020012503' slug='dyPrdNN' %}