# Overview
In this section, we'll be covering the basics of databases, SQL, and ORMs. We'll essentially start with a broad overview and end with how we query and manipulate database objects in our Rails app.

### What are Databases
Databases are collections of tables. Each 2-dimensional table has many fields (columns) and entries (rows). We use "Simple Query Language" aka SQL as the standard language to interact with our MySQL database. It provides many different interfaces to manipulate and query our database. When we run `mysql -u root -p` we are starting up our `sql-server` which holds many databases.

We can use SQL to check out the following:
- `use thecourseforum_development;`
- `show databases;` displays what databases we have
- `show tables;` lists tables in database `database`
- `describe table;` describes the fields of table `table`

##### What does it mean to be Relational?
This means that our database can handle relationships among tables. In our case, we have a bunch of real-world objects that are closely connected to each other. Students take classes that happen during certain semesters and are taught by different professors. Relational databases allow us to use what are called `join tables` to connect these objects together. For example, we have `courses` and `professors` tables as well as a `courses_professors` table which maps the two together.

This is in contrast to NoSQL databases such as MongoDB which are essentially lists of key-value stores. Each object is self-contained which makes for fast querying, but can't handle relations.

### Querying Databases
In this tutorial we'll focus mostly on querying databases rather than manipulating them. We just want to give you the tools to explore the data. For that reason, we'll be focusing on SQL `SELECT` queries.

Let's start with something basic:
```sql
SELECT * FROM users LIMIT 10;
```
The above command queries the students table for all of its fields and returns 10 results. But, what if we want to get all students with the first name Alice? And maybe we only care about their email.
```sql
SELECT email FROM users WHERE first_name = "Alice";
```
With the `WHERE` keyword we can specify values we'd like to filter by. A where clause can include boolean logic such as `AND` and `OR` as well.

Now what if we wanted to find all users with the first name Alice who are graduating in 2017? The `users` table doesn't have a field for graduating year, because users aren't necessarily students. Therefore, we need to run a join on the `users` and  `students` table.
```sql
SELECT u.email FROM users u INNER JOIN students s ON u.id = s.user_id WHERE u.first_name = "Alice" AND s.grad_year = 2017;
```
While there are other types of joins such as left and right coinciding with a venn diagram, you'll really only need to worry about `INNER JOIN`'s.

This has all been great for querying individual objects, but what about aggregate functions, like finding the max or min values of a field? SQL has the following such functions:
- `COUNT(*)`
- `MAX()`
- `MIN()`
- `SUM()`
- `AVG()`

So, for example, we can get the number of users with the name Alice:
```sql
SELECT count(*) FROM users WHERE first_name = "Alice";
```

Depending on the database type you're running, other aggregates may be included.
#### Practice Time:
Run through the following queries to get some practice (feel free to do your own once you get started!):
1. How many Subdepartments are there?
2. How many courses are there in the CS department?
3. What are the names of the professors who have taught ECON 2010?
4. How many perfect reviews (5 in all categories) do we have?
5. What's the max number of reviews a user has written and when do/did they graduate?
6. What's the average number of reviews users write?

A little harder:
1. Find the Subdepartment with the most courses.
2. Find the Subdepartment with the most total capacity.


### Dealing with Objects in Rails
Rails uses the ActiveRecord ORM, or Object-Relational Mapping, to work with our database objects directly within our controllers, etc. We'll go through this in the code.
