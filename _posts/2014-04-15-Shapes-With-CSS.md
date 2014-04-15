---
layout: post
title: Creating shapes with CSS 
description: "Blog about creating shapes with CSS."
modified: 2014-04-15
tags: [shapes with css]
image:
  feature: abstract-6.jpg
  credit: dargadgetz
  creditlink: http://www.dargadgetz.com/ios-7-abstract-wallpaper-pack-for-iphone-5-and-ipod-touch-retina/
comments: true
share: true
external: false
---
# Good Day~       
CSS is a style sheet language that is use to style the look and format of a document written in markup language. We could also use CSS to create a lot of different shapes. In order to create shapes using CSS, you would need to create a div element in HTML. A div element is essentially a rectangle/square. There are two types of div element that you can create; a "div id" or a "div class". The important thing to note about the differences between a "div id" and a "div class" is that the id selector takes precedence over class selector. There is a good discussion thread in <a href="http://stackoverflow.com/questions/544010/css-div-id-vs-div-class" title="css-div-id-vs-div-class" target="_blank">stack overflow</a> that discuss about the differences between using "div id" vs "div class". 
The example below shows how to create a circle with CSS.

{% highlight html linenos %}
{% raw %}
<!DOCTYPE html>
<head>
<style>
.circle
{
    width: 200px;
    height: 200px;
    background: blue;
    -moz-border-radius: 100px;
    -webkit-border-radius: 100px;
    border-radius: 100px;
}
</style>
</head>

<body>
<div class="circle"></div>
</body><!--end div circle-->
{% endraw %}
{% endhighlight %}

Below are some shapes demo that I have created using <a href="http://jsfiddle.net/" title="jsfiddle" target="_blank">jsfiddle</a>.

* <a title="Circle Demo" href="http://jsfiddle.net/7rUAK/2/" target="_blank">Circle Demo</a> 
* <a title="Semi-Circle Demo" href="http://jsfiddle.net/dC5D8/" target="_blank">Semi-circle Demo</a>

While writing this blog, I came across a good reference for creating shapes in css-tricks;
<a href="http://css-tricks.com/examples/ShapesOfCSS/" title="ShapesOfCSS" target="_blank">ShapesOfCSS</a>. This site contains lots of different shapes created using CSS. Put on you creative hat and start creating shapes with CSS!
I created an Android Robot. What about you?

<div markdown="0"><a href="http://htmlpreview.github.io/?https://github.com/christineoo/christineoo.github.io/blob/master/android-robot-example/android_robot.html" class="btn btn-info">Android Robot</a></div>

