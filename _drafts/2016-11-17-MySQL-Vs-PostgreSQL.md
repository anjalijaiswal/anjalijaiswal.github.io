---
layout: post
title: MySQL Vs PostgreSQL
date: 2016-01-01
comments: true
---

Many people have doubts when to go for MySQL and when to choose PostgreSQL. Here is a comparison of MySQL and PostgreSQL databases, offered not for the sake of voicing my opinion, but to help you make your own decision.

When to use MySQL
Why would you use MySQL over PostgreSQL? First, we need to consider the needs of the applications in terms of database requirements. If I want to create a Web application and performance is an issue, MySQL will be my choice because it’s fast and designed to work well with Web-based servers. However, if I want to create another application that demands transactions and foreign key references, PostgreSQL is the choice.

Let me suggest some reasons for using MySQL over PostgreSQL:
MySQL is relatively faster than PostgreSQL.
Database design will be simpler.
You can create a basic Web-driven Web site.
MySQL’s replication has been thoroughly tested.
There’s no need for cleanups in MySQL (Vacuum).

When to use PostgreSQL
PostgreSQL offers many advantages over MySQL.

For example, some of the features I use are foreign key references, triggers, and views. They allow me to hide the complexity of the database from the application, thus avoiding the creation of complicated SQL commands. I know many developers who prefer the rich functionality of PostgreSQL’s SQL commands. One of the most notable differences between MySQL and PostgreSQL is the fact that you can’t do nested subqueries of subselects in MySQL. PostgreSQL follows many of the SQL ANSI standards, thus allowing the creation of complex SQL commands.

Let me suggest some reasons for using PostgreSQL over MySQL:
Complex database design
Moving away from Oracle, Sybase, or MSSQL
Complex rule sets (i.e., business rules)
Use of procedural languages on the server
Transactions
Use of stored procedures
Use of geographical data
R-Trees (i.e., used on indexes)
