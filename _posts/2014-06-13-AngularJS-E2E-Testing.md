---
layout: post
title: AngularJS - E2E Testing with Protractor
description: "Blog post about E2E Testing with Protractor in AngularJS"
modified: 2014-06-13
tags: angularjs 
image:
  feature: abstract-10.jpg
comments: true
share: true
---

# Why test?

Website complexity has been growing enormously and manual testing is becoming more and more difficult to catch errors that might be introduced from our code. However, testing should not be neglected as writing effective test would in turn help us to make sure that our code is working correctly as intended.

It also gives us the opportunity to catch and fix errors before deploying to production. Writing test also helps the developer to understand each piece of the code better and would have an overall big picture of how each piece of code works together.

The good news is that AngularJS is written with testing in mind. Check-in of Angular source is tested before it is being accepted into the core. This blog post will talk about E2E(End-to-End) testing. E2E testing is testing from the end user's perspective of how our code should work. In AngularJS, E2E testing is done using Protractor. 

# Protractor

Protractor is built on top of Selenium's [WebDriverJS](https://code.google.com/p/selenium/wiki/WebDriverJs). The [Protractor Project](https://github.com/angular/protractor) is public in Github. Anyone can follow the project issues and help out the community.

Protractor is integrated with [Jasmine](http://jasmine.github.io/), thus E2E and unit testing can both be written using Jasmine. In Protractor, tests are run against your application that is running in a real browser and test scripts interact with the running browser like a user would.

# Install Protractor
<span style="color:blue;">**Step1:**</span> Install [NodeJS](http://nodejs.org/)

<span style="color:blue;">**Step2:**</span> Install Protractor globally 
{% highlight html %}
$ npm install protractor -g 
{% endhighlight %}    
*Note: `sudo npm install protractor -g` if you are having permission issue.*

<span style="color:blue;">**Step3:**</span> Run Selenium installation script from `node_modules/` directory.
{% highlight html %}
$ ./node_modules/protractor/bin/webdriver-manager update 
{% endhighlight %} 
    

<span style="color:blue;">**Step4:**</span> Start standalone Selenium server with the following command:
{% highlight html %}
$ ./node_modules/protractor/bin/webdriver-manager start
{% endhighlight %} 
*Note: [Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) is required in order to start Selenium server.*

Once installation is completed, the `protractor` command is now available. You can type in `protractor --help` to checkout the options available.

#Configuration
Protractor needs a configuration file to tell it which tests to run, how to connect a webdriver server and set options for reporting. You can take a look at [referenceConf.js](https://github.com/angular/protractor/blob/master/referenceConf.js) to see a complete list of configurations that are available to be used. 

If the referenceConfig.js is too much for you to digest, there are example configuration files located at `./node_modules/protractor/example` which are more concise and you may add things along when needed.
Below is an example of the `chromeOnlyConf.js` example taken from the example folder.
{% highlight javascript linenos %}
{% raw %}
// An example configuration file.
exports.config = {
  // Do not start a Selenium Standalone sever - only run this using chrome.
  chromeOnly: true,
  chromeDriver: '../selenium/chromedriver',

  // Capabilities to be passed to the webdriver instance.
  capabilities: {
    'browserName': 'chrome'
  },

  // Spec patterns are relative to the current working directly when
  // protractor is called.
  specs: ['example_spec.js'],

  // Options to be passed to Jasmine-node.
  jasmineNodeOpts: {
    showColors: true,
    defaultTimeoutInterval: 30000
  }
};
{% endraw %}
{% endhighlight %}

In line 14, `specs: ['example_spec.js']` is an example of test written in Jasmine. This file is also available in the example folder.  You can specify more than one file to test under the `specs` option. For example:
{% highlight javascript linenos %}
{% raw %}
specs: [
    'example_spec.js',
    'main_spec.js'
],

{% endraw %}
{% endhighlight %}
Protractor will execute the tests sequentially, meaning that `example_spec.js` will run first followed by `main_spec.js`

Now that you have your configuration file and test written. You just need to run 2 commands to start testing your application.

<span style="color:blue;">**Command #1:**</span>
{% highlight html %}
$ ./node_modules/protractor/bin/webdriver-manager start
{% endhighlight %} 

In a new Terminal window, run your configuration file.

<span style="color:blue;">**Command #2:**</span>
{% highlight html %}
$ protractor chromeOnlyConf.js
{% endhighlight %} 

You are all set. Hope you enjoy testing your AngularJS application!

# References

* [Slides on testing with Protractor](http://ramonvictor.github.io/protractor/slides/#/)
* [Practical End-to-End Testing with Protractor](http://www.ng-newsletter.com/posts/practical-protractor.html)
* [AngularJS Protractor E2E Cheatsheet](http://webslainte.blogspot.com/2014/01/angular-js-protractor-e2e-cheatsheet.html)
