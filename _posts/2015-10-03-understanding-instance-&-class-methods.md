---
title: Understanding Instance & Class methods
layout: post
modal-id: 6
date: 2015-10-03
project-date: October 2015
category: Web Development
description: Difference between Instance and class methods
analytics: true
comments: true
---

In programming world it’s often how we think about a particular problem that causes it not to work as we expected!
For example, a method can never be an instance or a class, instead a method is accessible via instance or class.
Let’s take this instance :

{% highlight ruby linenos %}
class Example
  def self.class_method
    instance_method # It will throw NoMethodError
  end

  def instance_method
    # some data
  end
end
{% endhighlight %}


So, why did it throw an error, there is definitely a method called instance_method. What's happening here? Actually ruby is searching for a class method, because ruby will read it as 'self.instance_method'. Here self is the "class" itself, hence the error.

Points to ponder:

  - Class methods do not have access to instance methods or instance variables. However instance methods can access both class methods and class variables.
