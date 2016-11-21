---
layout: post
title: Create Migrations Like A Pro!
date: 2015-12-05
comments: true
analytics: true
---

There are certain times when you want to change the schema of your rails application database or
want to drop the database altogether or while creating a new model you want to check if particular datatype is supported and whatnot! The list goes on. Hence i pulled some of them together in one place.

Here are some common migration commands which i use frequently, they might help you too :)

**Add a colomn in table via rails migration:**
{% highlight ruby linenos %}
  rails generate migration AddFieldNameToTableName field_name:datatype

  # example
  rails generate migration add_email_to_users email:string

  # This command will invoke change method:
  class AddEmailToUsers < ActiveRecord::Migration
    def change
      add_column :users, :email, :string
    end
  end
{% endhighlight %}

**Remove a colomn in table via rails migration:**
{% highlight ruby linenos %}
  rails generate migration RemoveFieldNameFromTableName field_name:datatype
  # example
  rails generate migration remove_name_from_users name:string
{% endhighlight %}

Currently the change method(used for changing existing tables) supports only these migration definitions:

* **add_column**
* **add_index**
* **add_timestamps**
* **create_table**
* **remove_timestamps**
* **rename_column**
* **rename_index**
* **rename_table**

Also Active Record supports the following database column types:

* :binary
* :boolean
* :date
* :datetime
* :decimal
* :float
* :integer
* :primary_key
* :string
* :text
* :time
* :timestamp

Besides migrations here are some common rake tasks on db:

* **db:create** creates the database for the current env
* **db:create:all** creates the databases for all envs
* **db:drop drops** the database for the current env
* **db:drop:all** drops the databases for all envs
* **db:migrate** runs migrations for the current env that have not run yet
* **db:migrate:up** runs one specific migration
* **db:migrate:down** rolls back one specific migration
* **db:migrate:status** shows current migration status
* **db:rollback** rolls back the last migration
* **db:forward** advances the current schema version to the next one
* **db:seed** (only) runs the db/seed.rb file
* **db:schema:load** loads the schema into the current env's database
* **db:schema:dump** dumps the current env's schema (and seems to create the db as well)

More detailed info:

* db:setup runs db:schema:load, db:seed
* db:reset runs db:drop, db:setup
* db:migrate:redo runs (db:migrate:down db:migrate:up) or (db:rollback db:migrate) depending on the specified migration
* db:migrate:reset runs db:drop db:create db:migrate

**Caution:
In seed file, always do a find_or_create_by to avoid duplication.**
