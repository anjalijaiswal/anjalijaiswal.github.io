---
layout: post
title: Understanding Rspec Doubles
date: 2016-09-27
comments: true
---

In this post we are exploring Rspec doubles. Basically double is any object that stands in for a real object during a test
(think "stunt double"). You create one using the double method.

`goal = double(Goal)` - will create an instance of a Rspec double class, which we can use to stand in for an instance of `Goal` class.
The argument for `double()`(normal double*) may or may not exist, thus `double('VirtualGoal')` is valid.

There are several benefits of using doubles:
   1. We do not need to create an instance of a real `Goal` class.  
   2. We can use the stub method on the double to simulate required behaviour, e.g. `goal.stub(:size).and_return('7.32x2.44')`.  
   3. You can use the stub as a spy, to assert calls and arguments to stubbed out methods, e.g.  
    `expect(my_stub).to receive(:stubbed_method).at_least(5).times.with({ arg_1 : 'val_1', arg_2: 'val_2 })`
   4. And you can always call the original method implementation with
    `allow(:my_stub).to receive(:stubbed_method).and_call_through`  
   5. We can define a hash for allowed messages and return values, e.g.

   {% highlight ruby linenos %}
    RSpec.describe "A test double" do
      it "returns canned responses from the methods named in the provided hash" do
        goal = double(Goal, foo: 3, bar: 4)
        expect(goal.foo).to eq(3)
        expect(goal.bar).to eq(4)
      end
    end
   {% endhighlight %}


In Rspec 3 and onwards Doubles are "strict" by default i.e. any message you have not allowed or expected will trigger an error

{% highlight ruby linenos %}
RSpec.describe "A test double" do
  it "raises errors when messages not allowed or expected are received" do
    goal = double("goal")
    goal.foo
  end
end

# will raise an errors
#<Double "goal"> received unexpected message :foo with (no args)
{% endhighlight %}

You can read more about verifying doubles [here](https://relishapp.com/rspec/rspec-mocks/v/3-5/docs/verifying-doubles/using-an-instance-double){:target="_blank"}
and normal doubles [here](https://relishapp.com/rspec/rspec-mocks/v/3-5/docs/basics/test-doubles){:target="_blank"}
