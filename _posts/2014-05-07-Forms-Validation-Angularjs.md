---
layout: post
title: AngularJS - Form Validations
description: "Blog post about form validation in AngularJS"
modified: 2014-05-07
tags: angularjs 
image:
  feature: abstract-5.jpg
comments: true
share: true
---

Form Validations

Today we'll talk about form validations in AngularJS. AngularJS provides one of the coolest feature of form validations at the client-side. This type of validation would allow instant feedback on the state of the form as users are filling up the form. Some of the common form validations that are always handy are such as:

* Required field
* Minimum and maximum allowed length
* Valid email
* Show error message to let user know what is the requirement needed
* Disable submit button when there are any errors detected

AngularJS allow us to implement form validations without a lot of extra work. Form validations are implemented using html5 tags or AngularJS directives. Developers can also create their own custom validations in AngularJS. Let's take a look at some examples below:-

### Required
To set an input field as a required input, a html5 `required` tag can be used.
{% highlight html %}
<input type="text" required>
{% endhighlight %}

### Matching a predefined regex pattern
AngularJS has a `ng-pattern="/eg-pattern/"` directive to ensure that the input matches with the predefined (regex)regular expression pattern.
{% highlight html %}
<input type="text" ng-pattern="/^[a-zA-Z]+$/">
{% endhighlight %}

### Minimum Length - ng-minlength
To set the minimum length requirement, we use `ng-minlength={number}`. The example below sets the minimum required length to be 3 characters.
{% highlight html %}
<input type="text" ng-minlength=3>
{% endhighlight %}

### Maximum length - ng-maxlength
On the other hand, to set the maximum length requirement, we use `ng-maxlength={number}`. The example below sets the maximum required length to be 10 characters.
{% highlight html %}
<input type="text" ng-maxlength=10>
{% endhighlight %}

### Number
To limit the user to only input numbers, we can set the `input type` to `number`.
{% highlight html %}
<input type="number" name="age" ng-model="user.age">
{% endhighlight %}

### Email
An email can also be validated in the input field by setting the `input type` to `email`.
{% highlight html %}
<input type="email" name="email" ng-model="user.email">
{% endhighlight %}

### Url
Url validation lets us validate if the input field represents a url. We do this by setting the `input type` to `url`.
{% highlight html %}
<input type="url" name="homeurl" ng-model="user.twitter_url">
{% endhighlight %}


## AngularJS Form Properties - `$valid, $invalid, $dirty, $pristine`

Below are some of the AngularJS form properties that are useful in helping us to validate the form. Various information can be obtained from the properties when they are applied to a form or input.

|
|----
| Property      | ng-class      | Description  
|:-------------:|:-------------:|:------------
| $valid        | ng-valid      | **Boolean** - Indicate whether an item is currently **valid** based on the rules you set.
|----
| $invalid      | ng-invalid    | **Boolean** - Indicate whether an item is currently **invalid** based on the rules you set.
|----
| $dirty        | ng-dirty      | **Boolean** - True when the input/form has been used.
|----
| $pristine     | ng-pristine   | **Boolean** - True when the input/form has not been used yet.
|----
| 
{: rules="groups"}

In order to access these AngularJS properties, we can use the following method:

* Access the **form** : `<form-name>.<angular-property>`
  * Example : `myForm.$valid`
* Access an **input** : `<form-name>.<input-name>.<angular-property>`
  * Example: `myForm.name.$valid`

Below is an example of AngularJS form validations:

* [Example form validation](http://plnkr.co/edit/ipYf2T1cvMgxmAEYwJg8?p=preview)

In this example, bootstrap formatting style are used to style the form. The form requirements implemented in this example form are such as:

* Name field:
  * is a required field
  * minimum length is 3
  * maximum length is 20
  * only alphabets are allowed 
* Age field:
  * only numbers
  * minimum age is 10
  * maximum age is 200
* Email field:
  * valid email address 

Some takeaways from this example:

* Different error message can be printed to the user based on what error the user encounters.
* Bootstrap provides styling for the error fields such as `help-block` to print error messages in red text.
* Using AngularJS form properties to check for any errors on the input field.
* `ng-disabled` can be used to prevent user from submitting when there are errors.

