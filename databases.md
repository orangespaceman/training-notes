# Database notes

A few notes prepared while writing training courses...

Note that the following examples assume *MySQL* as the chosen database. Other relational databases will tend to use a similar logic, although with slightly different syntax.


## Why use a database?

When building web applications, we often use a database to store information

We want to store our application *data* separately from:

 - application *logic* (e.g. Ruby, Python)
 - *presentation* (e.g. HTML templates)


### Advantages

There are a number of advantages for separating information from presentation:

 - Easier to manage content without changing logic
 - Data can be re-used elsewhere
 - Data can be managed via an administrative tool (such as a *content management system*), with little or no technical knowledge required
 - Databases are optimised to store and retrieve data quickly


## Database essentials

A database is just a collection of one or more tables of data

 - Each table has a number of **columns** (or fields, attributes)
 - Each column has a specific **name**
 - Each column also has a data **type** (e.g. text, number, date/time, etc)
 - Data is stored in a table in **rows**
 - Each individual column within a row is called a **cell**

Database field names don't usually contain spaces. Conventions usually suggest making them all lower-case, using underscores to separate words

| id | column_1    | column_2 |
| ---|-------------|----------|
| 1  | row 1       | cell     |
| 2  | row 2       | lorem    |
| 3  | cell        | ipsum    |


## An example scenario

The following notes will be based around designing a database to meet an example scenario:

*Design a database for a web application that tweets a daily question and aggregates __@replies__. These tweets will be categorised into one or more categories*


## Database design process

We can design our database by following a few simple steps:

1. Decide on what data you want to store
2. Choose data types for each of these items of information
3. Normalise the data

These notes will then explain how to:

1. Create your database
2. Populate your database
3. Query your database


## Storing data

When designing a database, it is important to first decide what data we want to store.

If we were to imagine our example data in tabular form, we might have something like this:

| id | name | handle         | question         | answer        | categories     | date_added          |
|----|------|----------------|------------------|---------------|----------------|---------------------|
| 1  | Pete | blah           | Favourite Cheese | Edam          | serious        | 2013-03-21 18:34:23 |
| 2  | Rich | rich_xyz       | Favourite Prince | Fresh         | funny, winner  | 2013-03-21 19:25:16 |
| 3  | Nick | something      | Favourite Prince | TAFKAP        | serious, funny | 2013-03-21 20:12:01 |
| 4  | Mike | dangerous      | Favourite Cheese | Melted cheese | funny, winner  | 2013-03-21 19:25:16 |



## Choosing data types

This step identifies the possible values for the data

Data types control the way the data is stored in the database - to make it as efficient as possible

A few example data types:

* String (text):
  - Fixed length (up to 255 characters)
  - Variable length (up to 255 characters)
  - Text (over 255 characters)

* Numeric:
  - Integers - whole numbers
  - Decimal - not whole numbers
  - Date and time

(Exact data types can vary depending on the database used)

In our example scenario we might use the following data types:

 - **ID**: integer
 - **name**: variable length text
 - **handle**: variable length text
 - **question**: variable length text
 - **answer**: variable length text
 - **categories**: text
 - **date_added**: date and time


## Data normalisation

To normalise data is to remove the duplication of information, so each piece of information should be stored only once

Once we have removed repetition of data we have removed the possibility of inconsistencies

This ensures that the 'integrity' of the data is maintained.

*What this means:*

Any repetitive data should be stored in a separate database table

To normalise data also means to ungroup items of data, to separate them so each cell contains only a single item of data

*What this means:*

Any cells containing multiple items of data should be stored in a separate database table


***Further reading:***

 - [http://phlonx.com/resources/nf3/](http://phlonx.com/resources/nf3/)
 - [http://en.wikipedia.org/wiki/Database_normalization](http://en.wikipedia.org/wiki/Database_normalization)
 - [http://www.devshed.com/c/a/MySQL/An-Introduction-to-Database-Normalization/](http://www.devshed.com/c/a/MySQL/An-Introduction-to-Database-Normalization/)
 - [http://support.microsoft.com/kb/100139](http://support.microsoft.com/kb/100139)


### Limiting normalisation

In a fully normalised database, there should be no duplication of information.

However this can sometimes fragment or over-complicate the data, and unnecessarily separate items of information which then need to be brought together in order to answer queries.

The database designer may sometimes prefer to have a database which is not strictly normalised so as to simplify the system and/or improve query performance.

***Further reading:***

 - [http://www.keithjbrown.co.uk/vworks/mysql/mysql_p7.php](http://www.keithjbrown.co.uk/vworks/mysql/mysql_p7.php)
 - [http://www.codinghorror.com/blog/2008/07/maybe-normalizing-isnt-normal.html](http://www.codinghorror.com/blog/2008/07/maybe-normalizing-isnt-normal.html)


### Primary keys

In every table, we must identify (or create) a unique ID (known as a primary key)

A primary key has three requirements:

1. It must always have a value (it cannot be left blank)
2. Its value must never change
3. It must be unique

A primary key must be a unique value which enables us to identify a single row of data, and so access all other data related to it

If none of the items of data are unique, they cannot act as a primary key

The simplest primary key is an integer that gets incremented for each new row

Sometimes we will want to reference the primary key from one table in another table in order to identify a relationship between the two. If we do this, in the second table it is known as a *foreign key*


### Entities and Attributes

For any scenario where you want to use a database, you need to identify the Entities and Attributes

#### Entities

Should be representations of real-world objects - events, persons, places, things

e.g. projects, tasks, books, authors, publishers, products, ingredients...

Each entity should have its own table in the database

Not an easy science to correctly identify entities, it is dependant on the scenario and often subjective

Once we have identified the entities, we can create a database table for each


#### Attributes

Pieces of information which characterise and describe these entities

These become the fields/columns for each entity table in the database

Need to identify the name of the attribute - e.g. 'name', 'answer', 'category'

Need to identify the attribute 'type' - e.g. text, integer, date, etc

Need to decide whether the attribute is optional - can it be empty?

Can the attribute uniquely identify the entity?


### Example database tables

Here are three of our example tables:

***Questions table***

| id | question          | date_added          |
|----|-------------------|---------------------|
| 1  | Favourite Cheese? | 2013-03-21 18:34:23 |
| 2  | Favourite Prince? | 2013-03-21 18:34:23 |

***Users table***

| id |  handle        | name |
|----|----------------|------|
| 1  | blah           | Pete |


***Categories table***

| id | category |
|----|----------|
| 1  | Funny    |


### Relationships

It is important to identify the relationships between tables

There are three types of relationship:

1. One-to-one (1:1)
2. One-to-many (1:N)
3. Many-to-many (N:M)


#### One-to-many (1:N) relationships

To identify a one-to-many (1:N) relationship, we use primary key to foreign key matching.

We store the primary key of the 'one' as a foreign key in each of the 'many' items, establishing the relationship between them.

Matching keys in this way allows related information to be brought together from different tables when the database is queried.

In our example, questions:answers is a one-to-many relationship, for each question there are multiple answers, but each answer is only for one question

Instead of adding the question for each answer, we'll store question details in the *questions* table

We'll add a new field to the answers table called question_id - here we'll put in the unique primary key from the question table as a foreign key in the answer table

Now the question details need only be stored once. If the question details were to change, we only need to update a single record in the question table and it would apply for all answers

In a similar manner, users:answers is also a one-to-many relationship. Each user can submit many answers, yet each answer can only be from a single user.

Here is our example *answers* table, including the use of foreign keys to tie our one-to-many relationships

***Answers table***

| id | question_id | user_id | answer | tweet_id    | date_added          |
|----|-------------|---------|--------|-------------|---------------------|
| 1  | 1           | 1       | Edam   | 23741876128 | 2013-03-21 18:34:23 |


#### Many-to-many (N:M) relationships

For a many-to-many (M:N) relationship, on both sides of the relationship there can be multiple entities in each table that are inter-related

For example, one answer may have several categories; one category may be applied to several answers.

To record this relationship we need to create a separate database table containing two foreign keys, which relate to the primary keys for each of the two relevant entities.

Here is our *answers to categories* join table

***Answers to Categories (join) table***

| id | answer_id | category_id |
|----|-----------|-------------|
| 1  | 1         | 5           |



## SQL

We have designed our database

We need to know how to create it, populate it and access this data

This is where we need SQL

Structured Query Language (SQL) is the language used by most databases to perform queries and manipulate data


### SQL rules

A few SQL rules to bear in mind:

SQL is generally case insensitive...

...except for table and column names, which are usually case sensitive

By convention, SQL commands (e.g. `SELECT`, `UPDATE`) should be written in UPPERCASE

Like in most programming languages, string (text) values should be surrounded by quotes ('single' or "double")

Table and column names can optionally be surrounded by \` backticks - note that these are not the same as 'single quotes'

All commands should terminate with a semi-colon;


### Creating a database

If you were to have to create a new database yourself, you'd use the following command:

```
CREATE DATABASE `dbname`;
```

To see a list of all available databases you would enter:

```
SHOW databases;
```

To select a database you would enter:

```
USE `dbname`;
```

To delete a database you would enter:

```
DROP `dbname`;
```

***THERE IS NO UNDO***


### Creating database tables

We have already planned the structure for our database tables, now we need to turn these into SQL

To create a table, use the CREATE TABLE command using the following syntax:

```
CREATE TABLE `table_name` (
    `column_name` column_type column_attributes
);
```

Example syntax for our answers table:

```
CREATE TABLE `answers` (
    `id`          INT           NOT NULL AUTO_INCREMENT PRIMARY KEY,
    `question_id` INT           NOT NULL,
    `user_id`     INT           NOT NULL,
    `tweet_id`    VARCHAR(20)   NOT NULL,
    `answer`      VARCHAR(255)  NOT NULL,
    `date_added`  DATETIME      NOT NULL
);
```

Taking the example of the column called `id`:

```
`id` INT NOT NULL AUTO_INCREMENT PRIMARY KEY
```

 - It will contain an integer (INT)
 - This column is not allowed to be left blank (NOT NULL)
 - This column is to act as a unique identifier for entries in this table, so all values in this column must be unique (PRIMARY KEY).
 - If we don't specify a value when adding a new entry, pick a value that is one more than the highest value in the table so far (AUTO_INCREMENT)

Within a database, you can request to see what tables exist:

```
SHOW TABLES;
```

You can also request to see the structure of a specific table:

```
DESCRIBE `tablename`;
```

It is possible to update the structure of an existing database table using the ALTER command

To add a column:

```
ALTER TABLE  `tablename` ADD `columnname` TEXT NOT NULL;
```

To update the name or attributes of a column:

```
ALTER TABLE  `tablename` CHANGE  `oldcolumnname` `newcolumnname`
VARCHAR(255);
```

To remove a column:

```
ALTER TABLE `tablename` DROP `columnname`;
```

To empty a table use the TRUNCATE command:

```
TRUNCATE TABLE `tablename`;
```

To delete a table use the DROP command:

```
DROP TABLE `tablename`;
```

***THERE IS NO UNDO***


### Example database tables

The following commands will create our example database tables:

```
CREATE TABLE `questions` (
    `id`          INT           NOT NULL AUTO_INCREMENT PRIMARY KEY,
    `question`    VARCHAR(255)  NOT NULL,
    `date_added`  DATETIME      NOT NULL
);

CREATE TABLE `users` (
    `id`          INT           NOT NULL AUTO_INCREMENT PRIMARY KEY,
    `handle`      VARCHAR(20)   NOT NULL,
    `name`        VARCHAR(255)  NOT NULL
);

CREATE TABLE `categories` (
    `id`          INT           NOT NULL AUTO_INCREMENT PRIMARY KEY,
    `category`    VARCHAR(255)  NOT NULL
);

CREATE TABLE `answers` (
    `id`          INT           NOT NULL AUTO_INCREMENT PRIMARY KEY,
    `user_id`     INT           NOT NULL,
    `question_id` INT           NOT NULL,
    `tweet_id`    VARCHAR(20)   NOT NULL,
    `answer`      VARCHAR(255)  NOT NULL,
    `date_added`  DATETIME      NOT NULL
);

CREATE TABLE `categories_answers` (
    `id`          INT           NOT NULL AUTO_INCREMENT PRIMARY KEY,
    `category_id` INT           NOT NULL,
    `answer_id`   INT           NOT NULL
);
```


### Populating a database

Our database and tables are now ready to go

We need to know how to populate them with data, and then retrieve this data

#### CRUD

Data-related tasks broadly fall into one of four categories:

 - Create (new data in a database)
 - Request/Read (data from a database)
 - Update (update existing data in a database)
 - Delete (data from a database)

SQL allows us to do just that:

 - Create = INSERT
 - Request =SELECT
 - Update = UPDATE
 - Delete = DELETE


#### INSERT

To add data to the tables we've just created, we use an INSERT command:

```
INSERT INTO `table_name` SET `columnName1` = 'value1', `columnName2` = 'value2';
```

(or)

```
INSERT INTO `table_name` (`columnName1`, `columnName2`) VALUES ('value1', 'value2');
```

The second version allows us to insert multiple rows (separated by commas) in a single SQL statement

```
INSERT INTO
  `table_name` (`columnName1`, `columnName2`)
VALUES
  ('value1', 'value2'),
  ('value1', 'value2'),
  ('value1', 'value2'),
  ('value1', 'value2'),
  ('value1', 'value2');
```


#### UPDATE

To update data in a table we use an UPDATE command:

```
UPDATE `table_name` SET `columnName1` = 'value1' WHERE `columnName2` = 'value2';
```

Note the use of the WHERE clause - without this all items in the table would be updated!


#### DELETE

To delete data from a table we use a DELETE command:

```
DELETE FROM `table_name` WHERE `columnName` = 'value';
```

Note the use of the WHERE clause - without this all items in the table would be deleted!

***THERE IS NO UNDO***


#### Populating our example database tables

```
INSERT INTO `categories` (`id`, `category`) VALUES
(1, 'Funny'),
(2, 'Serious'),
(3, 'Awkward'),
(4, 'Joke'),
(5, 'Winner');

INSERT INTO `categories_answers` (`id`, `category_id`, `answer_id`) VALUES
(1, 1, 1),
(2, 2, 2),
(3, 3, 2),
(4, 4, 1),
(5, 4, 3),
(6, 5, 3),
(7, 1, 4),
(8, 2, 4),
(9, 5, 5),
(10, 3, 6),
(11, 4, 6),
(12, 1, 7),
(13, 2, 8);

INSERT INTO `answers` (`id`, `user_id`, `question_id`, `tweet_id`, `answer`, `date_added`) VALUES
(1, 1, 1, '1347651374', 'Stilton', '2013-03-08 17:29:41'),
(2, 2, 1, '2374234', 'Melted', '2013-03-21 07:13:00'),
(3, 3, 2, '2378461216', 'Michael Fish', '2013-03-05 00:00:00'),
(4, 1, 2, '23746182376', 'humahumanukanukaapuaa', '2013-03-19 00:00:00'),
(5, 1, 3, '982736482764', 'Banned from the petting zoo', '2013-03-15 00:00:00'),
(6, 4, 3, '167312763512', 'Nothing', '2013-03-04 00:00:00'),
(7, 3, 4, '283746821364', 'Queen Latifah', '2013-03-20 00:00:00'),
(8, 4, 4, '71823182763', 'Rich', '2013-03-10 00:00:00');

INSERT INTO `questions` (`id`, `question`, `date_added`) VALUES
(1, 'What''s your favourite cheese?', '2013-03-03 15:30:23'),
(2, 'What''s your favourite fish?', '2013-03-20 15:29:38'),
(3, 'What''s the punchline to your favourite joke?', '2013-03-01 17:36:57'),
(4, 'Who''s your favourite queen?', '2013-03-09 19:45:42');

INSERT INTO `users` (`id`, `handle`, `name`) VALUES
(1, 'blah', 'Pete'),
(2, 'rich_xyz', 'Rich'),
(3, 'something', 'Nick'),
(4, 'dangerous', 'Mike');
```


### Querying a database

To read data from a table (or multiple tables) we use a SELECT command

The simplest SELECT command will return everything in a database table:

```
SELECT * FROM `table`;
```

Rather than returning everything, it is possible to specify just the field names (columns) you want:

```
SELECT `field` FROM `table`;
```

Multiple fieldnames are separated by commas:

```
SELECT `field1`, `field2`, `field3` FROM `table`;
```

Rather than returning all results, we can add optional parameters to filter our request using WHERE:

```
SELECT * FROM `table` WHERE `field` = 'value';
```

```
SELECT `field1`, `field2`, `field3` FROM `table` WHERE `field1` > value;
```

We can order our results using ORDER BY:

```
SELECT * FROM `table` ORDER BY `id`;
```

We can change the order using ASC or DESC:

```
SELECT * FROM `table` WHERE `field` > 100 ORDER BY `time` ASC;
```

We can limit the number of results returned using LIMIT:

```
SELECT * FROM `table` ORDER BY `time` LIMIT 2;
```

This will return the latest two records in the specified table

We can specify an offset to start the LIMIT from:

```
SELECT * FROM `table` ORDER BY `time` LIMIT 2, 2;
```

This will return two records, starting from record 3
(This is useful for pagination of results)

We can combine conditions using AND and/or OR:

```
SELECT
    `field1`, `field2`
FROM
    `table`
WHERE
    `field1` = 'lorem'
AND
    `field2` > 12
ORDER BY
    `time` ASC
```

#### Joining multiple tables

All of the SELECT examples so far have been on only a single table

When we normalised the data, we specifically moved content into separate tables

Now we need to know how to recombine it

We need to add clauses to match the primary keys and foreign keys

***Answers table***

| id | user_id | answer                                        | date_added          |
|----|---------|---------------------------------------------- |---------------------|
| 1  | 1       | lorem ipsum                                   | 2013-03-21 18:34:23 |
| 2  | 1       | quidquid Latine dictum sit altum videtur      | 2013-03-21 19:32:17 |
| 3  | 2       | Lorem ipsum dolor sit amet                    | 2013-03-21 20:31:25 |
| 4  | 3       | quidquid Latine                               | 2013-03-21 21:32:17 |
| 5  | 2       | ullamco laboris nisi ut aliquip ex ea commodo | 2013-03-21 22:31:25 |


***Users table***

| id | handle         | name |
|----|----------------|------|
| 1  | blah           | Pete |
| 2  | something      | Nick |
| 3  | dangerous      | Mike |


**SELECT with a join**

```
SELECT
  *
FROM
  `answers`
JOIN
  `users`
ON
  `answers`.`user_id` = `users`.`id`
```

| id | user_id | answer                                          | date_added          | handle          | name |
|----|---------|-------------------------------------------------|---------------------|-----------------|------|
| 1  | 1       | lorem ipsum                                     | 2013-03-21 18:34:23 | blah            | Pete |
| 2  | 1       | quidquid Latine dictum sit altum videtur        | 2013-03-21 19:32:17 | blah            | Pete |
| 3  | 2       | Lorem ipsum dolor sit amet                      | 2013-03-21 20:31:25 | something       | Nick |
| 4  | 3       | quidquid Latine                                 | 2013-03-21 21:32:17 | dangerous       | Mike |
| 5  | 2       | ullamco laboris nisi ut aliquip ex ea commodo   | 2013-03-21 22:31:25 | something       | Nick |


We can then add clauses, as before:

```
SELECT
  *
FROM
  `answers`
JOIN
  `users`
ON
  `answers`.`user_id` = `users`.`id`
WHERE
  `users`.`id` = 1
```

| id | user_id | answer                                          | date_added          | handle          | name |
|----|---------|-------------------------------------------------|---------------------|-----------------|------|
| 1  | 1       | lorem ipsum                                     | 2013-03-21 18:34:23 | blah            | Pete |
| 2  | 1       | quidquid Latine dictum sit altum videtur        | 2013-03-21 19:32:17 | blah            | Pete |


#### SELECT without joins

We could also recombine our data without explicitly using a JOIN

Technically this is the same as an inner join, but the syntax is slightly different...

```
SELECT
  *
FROM
  `answers`, `users`
WHERE
  `answers`.`user_id` = `users`.`id`
```

#### Multiple tables in a query

We have learnt how to query across multiple tables, by matching primary and foreign keys

When we query across multiple tables, the attributes from each table are flattened into a single table

There may be times when there are fields that we want to retrieve that have identical column names in more than one table (for example 'id')

If we try to do this, it will only retrieve one of the named columns - the other won't be present in the results

```
SELECT
  `questions`.`question`,
  `questions`.`id`,
  `answers`.`answer`,
  `answers`.`id`
FROM
  `questions`,
  `answers`
WHERE
  `questions`.`id` = `answers`.`question_id`
```

To resolve this we use AS in our SQL to alias the field names to something else, to make them unique

```
SELECT
  `questions`.`question`,
  `questions`.`id` AS `question_id`,
  `answers`.`answer`,
  `answers`.`id` AS `answer_id`
FROM
  `questions`,
  `answers`
WHERE
  `questions`.`id` = `answers`.`question_id`
```

***Further reading:***

 - [http://codular.com/sql-introduction](http://codular.com/sql-introduction)
 - [http://codular.com/mysql-joins](http://codular.com/mysql-joins)
 - [http://en.wikipedia.org/wiki/Join_(SQL)](http://en.wikipedia.org/wiki/Join_(SQL))
 - [http://www.keithjbrown.co.uk/vworks/mysql/mysql_p5.php](http://www.keithjbrown.co.uk/vworks/mysql/mysql_p5.php)
 - [http://www.coderecipes.net/sql-join-inner-join-left-join.aspx](http://www.coderecipes.net/sql-join-inner-join-left-join.aspx)


#### Retrieving Random Results With MySQL

You can select a random entry from a MySQL table using the SQL `RAND()` command

Add `ORDER BY RAND() LIMIT 0,1` to the end of a query:

```
SELECT * FROM `questions` ORDER BY RAND() LIMIT 0,1
```

Could be useful for selecting a random question to feature on a page


#### Grouping results

If you wanted to select a list of all answers for each question, you could perform the following query:

```
SELECT
  `questions`.`question` ,
  `answers`.`answer`
FROM
  `questions` ,
  `answers`
WHERE
  `questions`.`id` = `answers`.`question_id`
```

This will produce the following results:

| question         | answer        |
|------------------|---------------|
| Favourite Cheese | Edam          |
| Favourite Prince | Fresh         |
| Favourite Prince | TAFKAP        |
| Favourite Cheese | Melted cheese |

This will repeat the question each time for each answer

To group the answers together in a single column:

```
SELECT
  `questions`.`question ,
  GROUP_CONCAT(`answers`.`answer` SEPARATOR ', ') AS `answer_list`
FROM
  `questions` ,
  `answers`
WHERE
  `questions`.`id` = `answers`.`question_id`
GROUP BY `questions`.`id`
```

This will produce the following results:

| question         | answer              |
|------------------|---------------------|
| Favourite Cheese | Edam, Melted cheese |
| Favourite Prince | Fresh, TAFKAP       |


If you want to perform complex queries on your database, it is also worth investigating different types of database joins and sub-queries


#### Formatting A Date With MySQL

We've been storing dates in MySQL using the 'date', 'time' and 'datetime' data types

When these are retrieved from MySQL:

```
SELECT `date_added` FROM `answers`;
```

The output is in the format: "2012-02-27 15:20:29"

If you want to format this you can use DATE_FORMAT

```
SELECT DATE_FORMAT(`date_added`, '%e/%c/%y, %k:%i' AS `date_added_formatted` FROM `answers`;
```

***Further information:***

 - [http://dev.mysql.com/doc/refman/5.0/en/date-and-time-functions.html#function_date-format](http://dev.mysql.com/doc/refman/5.0/en/date-and-time-functions.html#function_date-format)


## Practice

Try to write the SQL queries that would satisfy the following requests:

 - Select all questions
 - Select all answers for user 1
 - Select all answers ordered by date answered
 - Select all answers for question 1, including the username of the person who answered
 - Select all answers from category 1
 - Select all answers from the category 'funny'
 - Select all answers for question 1, including the username of the person who answered and its category
