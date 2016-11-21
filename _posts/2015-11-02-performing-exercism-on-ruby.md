---
layout: post
title: Performing Exercism on Ruby!
date: 2015-11-02
comments: true
analytics: true
---

One day i stumbled upon this awesome site called **["Exercism.io"](http://exercism.io/){:target="_blank"}**. It mainly focuses on improving your skills via **Deep Practice & Crowdsourced Mentorship**, Strengthening your problem-solving skills by guiding others through the process. I got hooked onto it and  then i thought why not share my learnings with you all. One alert though, i am a ruby programmer so they are mostly ruby based.

**Things To Keep In Mind:**
===========================

Before tackling any program/problem/challenge you should keep certain points in your mind. Some are general, some are more language specific & here they are:

  * **Some questions you might want to ask yourself:**

    * >1. Am I adhering to the Single Responsibility Principle?
    >2. Is all my code on the same abstraction level?
    >3. Can I combine conditional clauses?
    >4. How does my API look to clients of this code (i.e. how do other classes interact with this class)?
    >5. Do I have duplication?
    >6. What requirements are likely to change? Would I be able to implement such changes painlessly? [Note that I am not saying that you should normally guess what future requirements are, but it can be helpful on exercism]

Use Private, that way you limit the public API of any class. It's considered a good practice to expose as few methods as possible, so you don't come up with a "fat interface" and has to maintain a lot of methods that probably nobody else uses (this is troublesome when you want to refactor your code but you aren't sure if somebody is using method x or not).


  * If you are using in-built methods you should understand them first, like how they are working, what are the pros & cons, in which use-case you should use them. Don’t assume dig them up. Some examples:

  * **Difference between p & puts:**
    `p foo` does `puts foo.inspect`, i.e. it prints the value of inspect instead of `to_s`, which is more suitable for debugging (because you can e.g. tell the difference between 1, "1" and "2\b1", which you can't when printing without inspect).

  * `to_a` is super-expensive on big ranges.

  * Use string interpolation only when necessary:

  {% highlight ruby linenos %}
    # Example where string interpolation is needed
    name = 'Anjali Jaiswal'
    puts "Welcome #{name}"

    # Example where string interpolation is not needed
    puts 'Hello World!'
  {% endhighlight %}

**Some problems from Exercism:**
================================
I have described what I learned from individual problem. I am also putting names of the relevant problems so that you can look them up. My code is uploaded on **["Github"](https://github.com/anjalijaiswal/exercism){:target="_blank"}**. Also I have explained why I used certain in-built Ruby methods. I have highlighted some specific things that you should consider in general.

**Accumulate:**
---------------
Two ways to yeild a block in ruby : **yield & call**  

{% highlight ruby linenos %}
# yield statement
def speak
  yield
end

# call statement
def speak(&block)
  puts block.call
end
{% endhighlight %}

* **read [“ZOMG WHY IS THIS CODE SO SLOW?”](http://confreaks.tv/videos/rubyconf2010-zomg-why-is-this-code-so-slow){:target="_blank"}**

* **a(&:upcase)** : you are passing a reference to the block (instead of a local variable) to a method. Also Symbol class implements the `to_proc` method which will unwrap the short version into it's longer variant.

* Yield returns the last evaluated expression (from inside the block). So in other words, the value that yield returns is the value the block returns.

* **If you want to return an array use map/select depending on situation. You dont need to intialize an array & return it.**

**Anagram:**
------------
Anagrams are same if sorted. Select will return element if condition satisfies. So in case of conditions use `select` over `map`/`each`.

**Beer-songs:**
---------------
[Follow this link](http://red-badger.com/blog/2014/08/20/i-spent-3-days-with-sandi-metz-heres-what-i-learned/){:target="\_blank"}

**Binary:**
-----------
Used `map.with_index` so no need to initialize another variable & directly apply `inject` on the result.

**Bob:**
--------
Start simple. Try to make test pass in a very easy way.

**Etl:**
--------
Use of `each_with_object`:

{% highlight ruby linenos %}
input.each_with_object({}) do |(score, letters), result|
  letters.each do |letter|
    result[letter.downcase] = score
  end
end
{% endhighlight %}

**Grade-school:**
-----------------
Initialize an empty hash & and declare values as an array. To sort & return a hash: `hash.sort.to_h`.

**Grains:**
-----------
Sometimes solution could be a single word. Check for patterns. For instance, here you don't have to iterate 64 separate calculations in self.total. Think about the totals for the first few squares: 1, 3, 7, 15, 31. Now think about those totals in relation to powers of two. Total is a series of (2x-1) where x is 2**(n-1).

**Hamming:**
------------

* `raise` could be another method. Always look out for **single responsibility principle.**

* `select` & `count` are perfect methods here.

* It is considered a good practice to **expose as few methods as possible**, so you don't come up with a "fat interface" and has to maintain a lot of methods that probably nobody else uses (this is troublesome when you want to refactor your code but you aren't sure if somebody is using method x or not). In this exercise, the only method being called is self.compute, so this means you could make `self.raise_size_mismatch` private and avoid exposing it.

**Hello-world:**
----------------

You can pass default argument to a ruby method :

{% highlight ruby linenos %}
def hello(name = 'world')
  #some data
end
{% endhighlight %}

**Leap:**
---------

You can minimize loop:
{% highlight ruby linenos %}
if year % 4 == 0 && year % 100 == 0
  year % 400 == 0 ? true : false
elsif year % 4 == 0
  true
else
  false
end
{% endhighlight %}

to:

{% highlight ruby linenos %}
year % 400 == 0 || year % 4 == 0 && year % 100 != 0
{% endhighlight %}

**Phone-number:**
-----------------

Intresting use of `sub`:

{% highlight ruby linenos %}
'0987654321'.sub(/(\d{3})(\d{3})/, "(\\1) \\2-") # will result in "(098) 765-4321"

# Can return a part of string like:
'0987654321'[0..2] # will result in '098'
{% endhighlight %}

**Raindrops:**
---------------

Assign common values as constant. Avoid unnecessary computing. For example you only need to check if 3,5 & 7 are factors.

**Robot-name:**
---------------

`shuffle` method of Array (Can be applied to a-z but will be futile for 0-999 as it takes lots of memory & computation). Use **Default assignment** `||=`

That’s it for now. Stay tuned for more of my technical musings. You can also mention in comments how this blog helped you or if i missed something that should be included. Sayonara for now!
