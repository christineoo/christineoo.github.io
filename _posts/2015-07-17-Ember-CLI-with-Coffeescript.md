---
layout: post
title: Ember CLI with CoffeeScript
description: "Ember CLI with CoffeeScript"
modified: 2015-07-17
tags: emberjs, coffeescript, ember-cli
image:
  feature: abstract-10.jpg
comments: true
share: true
---

# Setting Up Ember CLI with CoffeeScript

[Ember CLI](http://www.ember-cli.com/) is a powerful command line utility for Ember.js. By default, Ember CLI generates JavaScript files for your ember application. However, you can enable CoffeeScript easily.

Create a new Ember CLI application:

{% highlight html %}
$ ember new my-new-app
{% endhighlight %}

Next, install [ember-cli-coffeescript](https://github.com/kimroen/ember-cli-coffeescript) addon.

{% highlight html %}
$ ember install ember-cli-coffeescript
{% endhighlight %}

<small>Note: This addon requires Ember CLI version more than 0.2.0.

Let's modify the `app.js` to `app.coffee`

{% highlight coffeescript %}
{% raw %}
`import Ember from 'ember'`
`import Resolver from 'ember/resolver'`
`import loadInitializers from 'ember/load-initializers'`
`import config from './config/environment'`

Ember.MODEL_FACTORY_INJECTIONS = true

App = Ember.Application.extend
  modulePrefix: config.modulePrefix
  podModulePrefix: config.podModulePrefix
  Resolver: Resolver

loadInitializers(App, config.modulePrefix)

`export default App`
{% endraw %}
{% endhighlight %}

We are almost done. Now, let's modify `router.js` to `router.coffee`.

{% highlight coffeescript %}
{% raw %}

`import Ember from 'ember'`
`import config from './config/environment'`

Router = Ember.Router.extend
  location: config.locationType

Router.map ->

`export default Router;`

{% endraw %}
{% endhighlight %}

Lastly, run `ember server`. You should see "Welcome to Ember.js". The next time you use `ember generate` command, all files will be generated in CoffeeScript.

Now, you can start working on your ambitious web application using CoffeeScript!
