---
layout: post
title: Function Invocation - JavaScript 
description: "Types of Function Invocation"
modified: 2014-04-21
tags: [javascript]
image:
  feature: abstract-8.jpg
  credit: dargadgetz
  creditlink: http://www.dargadgetz.com/ios-7-abstract-wallpaper-pack-for-iphone-5-and-ipod-touch-retina/
comments: true
share: true
external: false
---

# Function Invocation in JavaScript

There are a few ways how we can invoke a function in JavaScript language. In this blog post, I am going to talk about the different types of function invocation in JavaScript.

##1. Invoke as A Function 
This is the most straight forward way of how functions can be invoked in JavaScript. The example below shows how functions can be declared and then invoked as a function.

{% highlight javascript linenos %}
{% raw %}
function hello() //method 1
{
  return "called hello";
}

var hi = function() //method 2
{
  return "called hi";
}

//invoke as a function
hello();
hi(); 
{% endraw %}
{% endhighlight %}

##2. Invoke as A Method
In JavaScript, an object can have a property that is assigned to a function. The function will then be invoked by referencing it through that property; i.e: invoke as a method of that object.
{% highlight javascript linenos %}
{% raw %}
var objectA = {}; //declaring an object
objectA.myFunction = function(){}; //create a myFunction property and assign it to a function.

//invoke as a method
objectA.myFunction();

{% endraw %}
{% endhighlight %}

##3. Invoke as A Constructor
Functions can be used as a constructor in JavaScript. The `new` keyword is used to invoke a function as a constructor.

{% highlight javascript linenos %}
{% raw %}
function Person(name)
{
  this.name = name;
}   

//invoke as a constructor
var person1 = new Person('Nancy');
{% endraw %}
{% endhighlight %}

When a function is declared as a constructor, the following occurs:

* A new object is created.
* `this` value of the constructor is assigned to the new object.
* Any properties available are added to the new object.
* Return the new object.

##4. Invoke using apply() and call() methods
The apply() and call() methods exist for every function in JavaScript. The apply() method is used by passing two parameters which are the object to be used as the function context and an array of values to be used as the invocation arguments. As for the call() method, an argument list is passed instead of an array.
{% highlight javascript linenos %}
{% raw %}
//using .apply() by passing an object and an array
myFunction.apply(object1,[]);
//using .call() by passing an object with an argument list
myFunction.call(object1,1,2,3);
{% endraw %}
{% endhighlight %}

All the above types of invocation are common in the JavaScript programming world. Knowing the different types of function invocation are crucial in understanding how `this` works in JavaScript. I will explain how `this` works in my next coming blog post. Stay tune!

