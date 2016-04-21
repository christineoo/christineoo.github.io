---
layout: post
title: Useful ES6 Features
description: "Useful ES6 Features for Javascript developer"
modified: 2016-04-21
tags: javascript, ES6, ECMAScript2015
image:
  feature: abstract-8.jpg
comments: true
share: true
---

1. Arrow function/Fat Arrow function - shorthand using `=>` syntax.

{% highlight javascript linenos %}
//*************** Before ES6 *********************//
var fullName = function(firstName, lastName){
  return firstName + lastName;
};

//*************** In ES6(using =>) ***************//
var fullName2 = (firstName, lastName) => {
  return firstName + lastName;
};

var fullName3 = (firstName, lastName) => firstName + lastName;

console.log(fullName("Bart ", "Simpson"));    //"Bart Simpson"
console.log(fullName2("Marge ", "Simpson"));  //"Marge Simpson"
console.log(fullName3("Maggie ", "Simpson")); //"Maggie Simpson"
{% endhighlight %}

The arrow syntax also omit the need for `var that = this` assignment or `.bind(this)`.

{% highlight javascript linenos %}
//*************** Before ES6 *********************//
var  customer = {
  name: "Jane Doe",

  handleMessage: function (message, handler) {
    handler(message);
  },

  greet: function () {
    var that = this;
    this.handleMessage("Hello, ", function(message){
      console.log(message + that.name);
    });
  }
};

customer.greet(); // "Hello, Jane Doe"

// Another option is to use .bind()
var  customer = {
  name: "Jane Doe",

  handleMessage: function (message, handler) {
    handler(message);
  },

  greet: function () {
    this.handleMessage("Hello, ", function(message){
      console.log(message + this.name); 
    }.bind(this));
  }
};

customer.greet(); // "Hello, Jane Doe"
{% endhighlight %}

Now, there is a simple way using the arrow function.

{% highlight javascript linenos %}
//*************** In ES6(using =>) ***************//
var  customer = {
  name: "Jane Doe",

  handleMessage: (message, handler) => handler(message),

  greet: function () {
    this.handleMessage("Hello, ", (message) => console.log(message + this.name));
  }
};

customer.greet(); // "Hello, Jane Doe"
{% endhighlight %}

2. Template Strings

{% highlight javascript linenos %}
//*************** Before ES6 *********************//
var salutation = "Hello";
var greeting = salutation + ", World";

console.log(greeting); // "Hello, World"

//*************** In ES6(using ${}) ***************//
var salutation = "Hello";
var greeting = `${salutation}, World`;

console.log(greeting); // "Hello, World"
{% endhighlight %}

You can also do computation inside `${}` such as the example below:
{% highlight javascript linenos %}
var  x = 1;
var  y = 2;
console.log(`${x} + ${y} = ${x+y}`); // 1 + 2 = 3
{% endhighlight %}

Another cool thing is multi-line string. Using backticks you can easily create a multi-line string.
{% highlight javascript linenos %}
var weatherNote = 'The weather\n\t'
    + 'today is\n\t'
    + 'sunny';

console.log(weatherNote);

//*************** In ES6(using ``) ***************//
var weatherNote = `The weather
    today is
    sunny`;

console.log(weatherNote);
{% endhighlight %}
 
3. let -  allows block scoping to be created.

{% highlight javascript linenos %}
//*************** Before ES6 *********************//
var x = 100;
if (x) {
  var x = 2;
}

console.log(x); // 2
//*************** In ES6(using let) ***************//
var x = 100;
if (x) {
  let x = 2;
}

console.log(x); // 100
{% endhighlight %}

4. const - assign constant variables that should not be re-assign
{% highlight javascript linenos %}
//*************** Before ES6 *********************//
var API_BASE_URL = "www.asdf.com";
API_BASE_URL = "qwer"; // still able to re-assign API_BASE_URL to another value
console.log(API_BASE_URL); // "qwer"

//************** In ES6(using const) *************//
const API_BASE_URL = "www.asdf.com";
API_BASE_URL = "qwer";
console.log(API_BASE_URL); // Will trigger an error saying attempting to override 'API_BASE_URL' which is a constant.
{% endhighlight %}



5. Spread Operator - the 3 dots `...`
{% highlight javascript linenos %}
//*************** Before ES6 *********************//
var fruits = ["strawberry", "orange", "apple"];
var moreFruits = ["pear", "grape"];
var allFruits = ["pineapple", fruits, "watermelon", moreFruits];

console.log(allFruits);
//allFruits returns ["pineapple", ["strawberry", "orange", "apple"], "watermelon", ["pear", "grape"]]

//*************** In ES6(using ...) ***************//
var fruits = ["strawberry", "orange", "apple"];
var moreFruits = ["pear", "grape"];
var allFruits = ["pineapple", ...fruits, "watermelon", ...moreFruits];

console.log(allFruits);
//allFruits returns ["pineapple", "strawberry", "orange", "apple", "watermelon", "pear", "grape"]
{% endhighlight %}


6. Default function parameters
{% highlight javascript linenos %}
//*************** Before ES6 ****************************************//
var multiplication = function(x, y){
  return x*y;
}

console.log(multiplication()); // NaN
console.log(multiplication(1, 2)); // 2

//*************** In ES6(default function parameters) ***************//
var multiplication = function(x=0, y=0){
  return x*y;
};

console.log(multiplication()); // 0
console.log(multiplication(1, 2)); // 2
{% endhighlight %}

7. Repeat
{% highlight javascript linenos %}
//*************** In ES6(.repeat()) ***************//
var cat = "meow".repeat(5);

console.log(cat); // "meowmeowmeow"
{% endhighlight %}

Below are some references that you can take a look to learn more about ES6.

References:

1. [Egghead](https://egghead.io/series/learn-es6-ecmascript-2015)
2. [lukehoban/es6features](https://github.com/lukehoban/es6features)
3. [Top 10 ES6 Features Every Busy JavaScript Developer Must Know](http://webapplog.com/es6/)
4. [MDN](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference)
