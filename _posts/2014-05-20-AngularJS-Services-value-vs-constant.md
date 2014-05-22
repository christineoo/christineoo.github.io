---
layout: post
title: AngularJS Services - value vs constant 
description: "Blog post about value vs constant in AngularJS"
modified: 2014-05-20
tags: angularjs 
image:
  feature: abstract-6.jpg
comments: true
share: true
---

Services

In AngularJS, there are five different service types.

* value
* constant
* factory
* service
* provider

Each type of services has its own unique characteristics that makes it useful for handling a certain type of problems. This blog post will talk about value and constant services.

##`value`

`value` is the simplest of all services. A value service literally provides predefined value to the object.
Below is the `service.js`. Here we defined a value called `message` that contains the string `"Hello world from value!"`
{% highlight javascript linenos %}
{% raw %}
//service.js
angular.module("services", [])
	.value("message", "Hello world from value!");
{% endraw %}
{% endhighlight %}

`main.js` below defines the controller for this app. Notice that `services` module is injected to this module. This is required because the components defined in the `services` module are by default not accessible by the `root` module. Line 2 means that the `root` module depends on the `services` module to work.  
{% highlight javascript linenos %}
{% raw %}
//main.js
angular.module("root", ["services"])
	.controller("index", ["$scope", "message", function($scope, message) {
		$scope.message = message;
	}]);
{% endraw %}
{% endhighlight %}


Lastly, is the `index.html` that will print the `message` defined by the `value` in  `service.js`. This `index.html` will be used throughout this blog post.
{% highlight html linenos %}
{% raw %}
<!-- index.html -->
<!DOCTYPE html>
<html ng-app="root">
<head lang="en">
    <meta charset="utf-8">
    <title>Services-Constant-Value</title>
</head>
<body>
    <div ng-controller="index">
        <h1>{{message}}</h1>
    </div>
    <script type="text/javascript" src="https://ajax.googleapis.com/ajax/libs/angularjs/1.2.5/angular.min.js"></script>
    <script type="text/javascript" src="main.js"></script>
    <script type="text/javascript" src="service.js"></script>
</body>
</html>
{% endraw %}
{% endhighlight %}

##`constant`
Declaring `constant` is very similar to how you would declare a `value`. Below is an example of how `constant` is declared; referencing from the above example:
{% highlight javascript linenos %}
{% raw %}
.constant("message", "Hello World from constant!")
{% endraw %}
{% endhighlight %}

If you were to replace line 3 in the `service.js` with the above code, you will get `Hello World from constant!` printed out on your browser. You may be wondering what is the difference between `value` and `constant` then since both of them seems to perform similar task? 

The difference between them is that `constant` service is able to be injected to the `config()` but `value` cannot. This is because `config()` are executed before services are instantiated and therefore, we cannot inject the `value` service because it is yet to be created.

Now, we'll take a look at a more concrete example on how `constant` service is injected to the `config()`. The example below will output `Hello world from constant!` to your browser.

{% highlight javascript linenos %}
{% raw %}
//service.js
angular.module("services", [])
    //.value("message", "Hello world from value!")
    .constant("message", "Hello world from constant!")

    .provider("greet", function() {
        var type;
          return {
            setType: function (value) {
                type = value
            },
            $get: function(){
                return {
                  message: type,
                }
            }
          }
    })
{% endraw %}
{% endhighlight %}
 
{% highlight javascript linenos %}
{% raw %}
//main.js
angular.module("root", ["services"])
    .config(function (greetProvider, message) {
        greetProvider.setType(message)
    })
    .controller("index", function($scope, greet) {
        $scope.message = greet.message;
    });
{% endraw %}
{% endhighlight %}

Let's do some experiment and try to ***uncomment line 3*** and ***comment line 4***. Test out the code on your browser and see what happens.

You will not see the `Hello world from constant!` output anymore. If you take a look at your console you will see an [error message](https://docs.angularjs.org/error/$injector/modulerr?p0=root&p1=Error:%20%5B$injector:unpr%5D%20http:%2F%2Ferrors.angularjs.org%2F1.2.5%2F$injector%2Funpr%3Fp0%3Dmessage%0A%20%20%20%20at%20Error%20(nat)). This is because `value` service does not exits yet when the `config()` executes.

I'll discuss about the remaining three services ( factory, service and provider) in my [next post](http://christineoo.github.io/AngularJS-Services-factory-service-provider/). Stay tuned!
