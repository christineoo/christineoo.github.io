---
layout: post
title: Scope, context and 'this' - JavaScript
description: "Blog post about scope and this in JS"
modified: 2014-04-21
tags: [javascript]
image:
  feature: abstract-3.jpg
  credit: dargadgetz
  creditlink: http://www.dargadgetz.com/ios-7-abstract-wallpaper-pack-for-iphone-5-and-ipod-touch-retina/
comments: true
share: true
---


## Scope
There are two types of scopes in JavaScript; **local** and **global** scope. Any variables or functions that is declared outside of a function body is deemed a global scope. Global scope can be accessed and manipulated from any scope. On the other hand, variables and functions declared inside of a function body is deemed a local scope. Local scope can only be accessed and manipulated within the function body of which they are declared.

{% highlight javascript linenos %}
{% raw %}
var myVar = 'global variable';
console.log('myVar value before myScope function: '+ myVar); // prints global variable
function myScope()
{
    var myLocalVar = 'local variable';
    function myInnerScope()
    {
      var myInnerLocalVar = myLocalVar; // myLocalVar can be accessed from myInnerScope
      console.log(myInnerLocalVar); // prints local variable
      myVar = 'overwrite global'; // myVar is global variable, can be accessed from myInnerScope
      console.log('myVar value overwrite from myScope function: ' + myVar); // prints overwrite global 
    }
    myInnerScope();
    console.log(myLocalVar); // prints local variable 
    console.log(myInnerLocalVar); // undefined because myInnerLocalVar only can be accessed in myInnerScope
}

myScope(); // invoke the global function
{% endraw %}
{% endhighlight %}

Below is a simple illustration of the scope of variables and functions based on the above code example. From the illustration, you can clearly see that the myVar and myScope() are global scope and can be accessed from any of the local scopes. Note that the `myInnerLocalVar` has the most limited scope in this example and it can only be accessed inside `myInnerScope`.
![Scope javascript]({{ site.url }}/images/scope_javascript.png)
{: .center}


## Context
In the web browser environment, the global context belongs to the `window` object. Therefore, all global variables and functions are created as properties and methods for the `window` object. When an execution stack has executed all of its code, the variables and functions defined within that context will be destroyed. However, global context will not be destroyed until the user exits the application by closing the web page.

Function call in JavaScript will have its own execution context. You can visualize execution context as a stack whereby global context is the base of the stack and each function call will push a new execution context on top of the stack. When a function(f1) has finished executing, the f1 execution context will be popped and return the control to the previosly executing context. 

The execution context of a function object can be accessed using the `this` keyword. The usage of `this` is explain below.

## The `this` Keyword
Whenever a function is invoked in JavaScript, a list of parameters is passed to the called function as arguments. The `this` parameter is also passed implicitly to the called function. `this` keyword behaves differently in JavaScript compared to other programming languages. In JavaScript, `this` is determined by how a function is being invoked. Please refer to my earlier blog post about [types of function invocation in JavaScript](/Invoke-function-JavaScript/)

###1. First Example - Invoke as function
{% highlight javascript linenos %}
{% raw %}
var myVar;
console.log(myVar); //prints undefined
window.myVar = 10;
console.log(this.myVar); //prints 10
{% endraw %}
{% endhighlight %}

 The above example shows that the global variable, `myVar` is a property of the `window` object. An undefined result is obtained when `myVar` is declared without any value assigned to it. The `window.myVar = 10` assigns a value of 10 to the `myVar` property of the `window` object. Using `console.log(this.myVar)` will give the value of 10 because `this` is refering to the `window` object.

###2. Second Example - Invoke as method
{% highlight javascript linenos %}
{% raw %}
var myObject = {
  myFunction : function()
  {
    return this; //this is refering to myObject
  }
};

console.log(myObject.myFunction() === myObject); // prints true
console.log(myObject.myFunction() === window); // prints false
{% endraw %}
{% endhighlight %}

`myFunction` is the method of the `myObject` object. `this` in this example is refering to `myObject` and not the `window` object. 

###3. Third Example - Invoke as constructor
{% highlight javascript linenos %}
{% raw %}
function Person(name)
{
  this.name = name;
  this.myFunction = function()
  {
    return this; //this refers to whichever object that calls the myFunction method
  }
}   

//invoke as a constructor
var person1 = new Person('Nancy');
var person2 = new Person('Peter');
console.log(person1.myFunction() === person1); // prints true
console.log(person2.myFunction() === person2); // prints true 
{% endraw %}
{% endhighlight %}

Whenever the `new` keyword is used to invoke a function, this means that the function is invoked as a constructor. Thus, `person1` and `person2` would have reference to the myFunction method available in the Person constructor. `this` in this example would refer to whichever object that calls the myFunction method. For example, if `myFunction()` is invoked by the `person1` object, then `this` refers to `person1`.

###4. Fourth Example - Invoke as call() and apply()
{% highlight javascript linenos %}
{% raw %}
function add()
{
  var sum = 0;
  for (var n = 0; n < arguments.length; n++)
  {
    sum += arguments[n];
  }  
  this.sum = sum; //this refer to the object parameter passed using the call() or apply() function
}

var price1 = {};
var price2 = {};
add.call(price1, 2, 5);
console.log(price1.sum); // prints 7
add.apply([price1, 2, 5]);
console.log(price1.sum); // prints 7

add.call(price2, 12, 2);
console.log(price2.sum); // prints 14
add.apply([price2, 12, 2]);
console.log(price2.sum); // prints 14

{% endraw %}
{% endhighlight %}
In this last example, call() and apply() are used to invoke the add function. The parameter of call() and apply() consists of the object name itself. Thus, we can explicitly specify the object that we would like to refer to when calling the add function.

When I was writing this blog post, I came across a few good references that I would like to recommend:
 
* [Professional JavaScript for Web Developers, 3rd Edition by Nicholas C. Zakas](http://www.amazon.com/Professional-JavaScript-Developers-Nicholas-Zakas/dp/1118026691)
* [Secrets of the JavaScript Ninja](http://www.amazon.com/Secrets-JavaScript-Ninja-John-Resig/dp/193398869X)
* [Understanding Scope and Context in JavaScript](http://ryanmorr.com/understanding-scope-and-context-in-javascript/)
