---
layout: post
title: Understanding PG HStore
date: 2016-01-01
comments: true
analytics: true
---

Sometimes we may need to not only store plain attributes like string, integer or boolean but also more complex objects in our databases. Like a key-value pair, so lets see how we can achieve it in Postgres - Rails with hstore.

HStore is a key value store within Postgres database. You can use it similar to how you would use a hash in Ruby application, though it’s specific to a table column in the database. If you need to think about possible use cases, please note that hashes in other languages are called dictionaries, so it’s already a hint how to and why use them.

So lets dive deep into the icy chill waters of hstore :P

We have a Model called "Leave" and it has a hstore column "applied". Lets suppose I have three types of leaves:

- CL: casual leave
- SL: sick leave
- LOP: loss of pay

(you can create as many keys as you wish)

So here 'LOP', 'SL' and 'CL' will act as my keys
{% highlight ruby linenos %}
  # If you will run ap Leave in console, you will get:
  class Leave < ActiveRecord::Base {
                 :id => :integer,
            :applied => :hstore,
         :created_at => :datetime,
         :updated_at => :datetime
  }
{% endhighlight %}

Now we will start with creating a Leave:
{% highlight ruby linenos %}
  leave = Leave.create(applied: {"LOP" => 2, "SL" => 2, "CL" => 0})
  #<Leave id: 1, applied: {"LOP" => 2, "SL" => 2, "CL" => 0}, created_at: "2016-01-01 11:16:47", updated_at: "2016-01-01 11:16:47">

  leave.applied
  # => {"LOP" => "2", "SL" => "2", "CL" => "0"}
{% endhighlight %}
**Please do keep in mind that hstore supports only string data.**

Find all Leaves with particular Leave Type:
{% highlight ruby linenos %}
  Leave.where("applied ? 'LOP'")

  # ('?' operator checks for a key in hstore)
{% endhighlight %}

Find Leaves with particular value of a Leave Type:
{% highlight ruby linenos %}
  Leave.where("applied -> 'LOP' = '2'")

  # OR

  Leave.where("applied @> 'LOP => 0.0'")

  # @> will check if left operand is contained in right?
{% endhighlight %}

Find Leaves with all specified keys:
{% highlight ruby linenos %}
  Leave.where("applied ?& ARRAY['LOP', 'CL']")
{% endhighlight %}

Find Leaves with any of the specified keys
{% highlight ruby linenos %}
  Leave.where("applied ?| ARRAY['LOP', 'CL']")
{% endhighlight %}

Now you know most of the queries which you can run with hstore. Do experiment with it. While we are on the same topic I would like to discuss an issue which I faced while creating a scope.

You can't pass an array as a variable in where clause, you have to pass it as a symbol. For instance I am getting leave types from params so they are user specific. Keep this in mind while querying and happy hashing.
{% highlight ruby linenos %}
  # leave_types_array = ['LOP', 'CL']
  scope :applied_leaves, -> (leave_types_array) { where('applied ?| ARRAY[:key]', key: leave_types_array)}
{% endhighlight %}


<!-- # scope :multi_allotments, -> (leave_definition_ids) { select("leave_allotments.id,leave_allotments.employee_id,adjusted -> ARRAY#{leave_definition_ids} as adjusted_tmp, alloted -> ARRAY#{leave_definition_ids} as alloted_tmp, lapsed -> ARRAY#{leave_definition_ids} as lapsed_tmp, opening_balance -> ARRAY#{leave_definition_ids} as opening_balance_tmp, allot_from -> ARRAY#{leave_definition_ids} as allot_from_tmp, allot_to -> ARRAY#{leave_definition_ids} as allot_to_tmp") }
  # Make sure leave_definition_ids are string;  ref: http://stormatics.com/howto-handle-key-value-data-in-postgresql-the-hstore-contrib/
  # scope :allotments_by_leave_type, -> (leave_definition_ids) { where('adjusted ?| ARRAY[:key] AND alloted ?| ARRAY[:key] AND lapsed ?| ARRAY[:key] AND opening_balance ?| ARRAY[:key] AND allot_from ?| ARRAY[:key] AND allot_to ?| ARRAY[:key]', key: leave_definition_ids) } -->
**Must read:**

* **[PG Docs Hstore](http://www.postgresql.org/docs/9.0/static/hstore.html)**

Reference:

* [How to handle key value data in postgresql via hstore](http://stormatics.com/howto-handle-key-value-data-in-postgresql-the-hstore-contrib/)

<!-- http://nandovieira.com/using-postgresql-and-hstore-with-rails -->

<!--   Dutylog.where("(properties -> '206B')::float > 0.0").sum("(properties -> '206B')::float")
-->

<!--  http://big-elephants.com/2012-10/aggregations-with-pg-hstore/ -->

<!--     # select alloted->leave_definition_id as leave_definition_id, sum(lapsed) as lapsed_total group by leave_definition_id, lapsed
 -->

 <!--  https://www.reddit.com/r/PostgreSQL/comments/1z1fb6/help_me_improve_this_query_summing_hstore_values/ -->

 <!-- https://gist.github.com/rapimo/3957743 -->
 <!--  -->
