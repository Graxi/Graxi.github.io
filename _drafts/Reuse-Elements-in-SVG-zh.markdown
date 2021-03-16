---
layout: post
title: '在SVG里复用元素'
categories: [Visualization]
permalink: /visualization/making-elements-reusable-in-svg
---  

在一个数据可视化的项目里，也许会有很多只有细微差别的元素，我们可以把它们看成是具备不同参数的同一个元素。比如在上一篇文章*[对SVG Path实现模糊focus的小技巧](https://subtleworks.cn/visualization/improve-svg-path-hover-sensitivity)*里，我提到过为目标路径创建一个更宽的透明外层，从而实现最终效果。   

{% include embed-codepen.html pen='2020012503' slug='dyPrdNN' %}

在建立透明外层的过程中，我们使用了`<use>`标签来复用事先在`<defs>`里定义好的元素。下面我们举个简单的例子一步步来看。  

#### 使用`<use>`标签复用元素

SVG提供了`<use>`标签来引用已经创建的元素。下面的例子里包含两条直线，上面的那条是原始元素，下面的那条是使用`<use>`标签复制的，相对于原始元素下移了50像素。   

{% include embed-codepen.html pen='2020022301' slug='mdJOLLj' %}

但是使用`<use>`标签会造成两个问题：
- 使用`<use>`标签只能复用元素，但无法修改元素的属性。
- 复用的元素坐标，即x和y属性的值，是相对于原始元素设定的。这意味着我们需要提前确定原始元素的位置。

#### 使用`<defs>`标签定义可修改属性的元素

基于以上情况，我们可以引入`<defs>`元素解决这两个问题。首先，定义在`<defs>`里的元素不会被显示；另外，当使用`<use>`标签复用元素时，既可以修改已定义元素的属性比如`stroke`和`stroke-width`，还可以为元素设置绝对坐标。     

需要注意的是，我们给`<use>`标签设置的绝对坐标会成为复制后的元素的零点坐标。  

{% include embed-codepen.html pen='2020022302' slug='ExjNGRZ' %}
