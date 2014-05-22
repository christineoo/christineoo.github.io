---
layout: post
title: AngularJS Services - factory, service, provider 
description: "Blog post about factory, service, provider in AngularJS"
modified: 2014-05-22
tags: angularjs 
image:
  feature: abstract-7.jpg
comments: true
share: true
---

Services

In my [previous blog post](http://christineoo.github.io/AngularJS-Services-value-vs-constant/), I talked about the differences between value and constant services. This blog post will continue to discuss the factory, service and provider services in AngularJS. 

##`factory`
`factory` is an AngularJS service that allows you to inject a function. The syntax for declaring `factory` service is as below:
{% highlight javascript linenos %}
{% raw %}
angular.module("services", [])
    .factory("factoryName", [function(){
       //function logic
    }])
{% endraw %}
{% endhighlight %}
`factory` comes in handy when you would like to inject a function instead of a `variable` that the `value` service provide. Below is a simple example of using factory to inject a function that returns the greet message, "Hello world from factory!".
{% highlight javascript linenos %}
{% raw %}
//service.js
angular.module("services", [])
    .factory("greet", function() {
        return {
            message: "Hello world from factory!"
        }
    })
{% endraw %}
{% endhighlight %}
{% highlight javascript linenos %}
{% raw %}
//main.js
angular.module("root", ["services"])
    .controller("index", function($scope, greet) {
        $scope.message = greet.message;
    });
{% endraw %}
{% endhighlight %}
If you would like to try this code on your browser, you can use the `index.html` from my previous [blogpost](http://christineoo.github.io/AngularJS-Services-value-vs-constant/).

##`service`
`service` is pretty much like `factory` whereby you can inject function using service. The difference is that in `service`, constructor function is injected and variables and methods are created with `this` keyword. An example of how a `service` is created is as below:
{% highlight javascript linenos %}
{% raw %}
angular.module("services", [])
    .service("serviceName", [function(){
    //function logic
    this.pi = 3.14;
    this.method1 = function(){
       //method1 logic
    } 
}])
{% endraw %}
{% endhighlight %} 
I have also created a simple service to print "Hello world from service!" in the example below:
{% highlight javascript linenos %}
{% raw %}
//service.js
angular.module("services", [])
    .service("greet", function() {
        this.message = function()
        {
            return "Hello world from service!";
        }
    })
{% endraw %}
{% endhighlight %}
{% highlight javascript linenos %}
{% raw %}
//main.js
angular.module("root", ["services"])
    .controller("index", function($scope, greet) {
        $scope.message = greet.message();
    });
{% endraw %}
{% endhighlight %}

##`provider`
Another useful AngularJS services is `provider`. It uses the `$get` method which is available in AngularJS. `provider` is a function that must return an object containing the `$get` property. 
Let's take a look at an example on how to use `provider` to print our "Hello world from Provider!" message.
{% highlight javascript linenos %}
{% raw %}
//service.js
angular.module("services", [])
    .provider("greet", function() {
        var type;
        return {
            setType: function (value) {
              type = value
            },
            $get: function(){
              return {
                message: type + "!",
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
    //the function argument needs to be the providerName + "Provider"
    .config(function (greetProvider) {
      greetProvider.setType("Hello world from Provider")
    })
    .controller("index", function($scope, greet) {
        $scope.message = greet.message;
    });
{% endraw %}
{% endhighlight %}
Things to note on this example is the `greetProvider`. We need to make sure that it matches the provider name that you have created and concatenate it with the `Provider` word in order for AngularJS to recognize it. Also, note that `provider` is able to be injected to config().

Below is a summary table of all the services I have discussed.

|----
|
|----
| **services**  ||| **use $get?**||| **present during configuration phase?**|||**present during run phase?**| 
|:-------------:|||:------------:|||:------------------------------------:|||:--------------------------:|
| constant      ||| No           ||| Yes                                  ||| Yes                        | 
|----                                                                                           
| value         ||| No           ||| No                                   ||| Yes                        |                     
|----                                                                                                    
| factory       ||| No           ||| No                                   ||| Yes                        |
|----                                                                                                    
| service       ||| No           ||| No                                   ||| Yes                        |
|----                                                                                                     
| provider      ||| Yes          ||| Yes                                  ||| No                         |
|----
|  
|---
{: rules="rows"}

Further recommended readings to learn more about services in AngularJS are listed below:

* [Angular.js: service vs provider vs factory?](http://stackoverflow.com/questions/15666048/angular-js-service-vs-provider-vs-factory)
* [Services](http://learn-angular.org/#!/lessons/handling-complexity)
* [Angular JS–Part 13, Services](http://lostechies.com/gabrielschenker/2014/02/26/angular-jspart-13-services/)

