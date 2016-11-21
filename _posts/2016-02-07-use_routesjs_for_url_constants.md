---
layout: post
title: Use routes.js for URL constants
date: 2016-02-07
comments: true
---

We have often heard the term 'Separation of concerns', we tend to decouple our app into a series of independent components, but do we really do it all the way? Give some thoughts †o it.

All of us have used ajax calls with our rails projects. This is how we generally do it:
{% highlight ruby linenos %}
$.ajax
  url: '/welcome'
  data: 'Hello User'
  type: 'GET'
  dataType: 'json'
{% endhighlight %}

We go directly and use urls as strings instead of making them a constant. I don't like hardcoding absolute URLs in my JavaScript code, it's bad practice anyway. So how can you make your urls as constant?

Lets say I am using CoffeeScript in my rails project. We will create a routes.js file in which we will  save all our routes which we want to use.

routes.js.coffee
{% highlight ruby linenos %}
# Make a global constant
window.DEFINE_ROUTE = {}
# Assign a value to 'welcomePath' property
Object.defineProperty DEFINE_ROUTE, 'welcomePath', value: '/welcome'
{% endhighlight %}

Now we can call our constant, 'DEFINE_ROUTE' in ajax call.

welcome.js.coffee
{% highlight ruby linenos %}
$.ajax
  url: DEFINE_ROUTE.welcomePath
  data: 'Hello User'
  type: 'GET'
  dataType: 'json'
{% endhighlight %}
