# SQL-cheatsheet
## Basics
### To select everything from a database:
```
SELECT * FROM celebs;
```
A relational database is a database that organizes information into one or more tables. Here, the relational database contains one table. 

A table is a collection of data organized into rows and columns. Tables are sometimes referred to as relations.
<hr>

### All data stored in a relational database is of a certain data type. Some of the most common data types are:

- INTEGER, a positive or negative whole number
- TEXT, a text string
- DATE, the date formatted as YYYY-MM-DD
- REAL, a decimal value
<hr>

### A statement is text that the database recognizes as a valid command. Statements always end in a semicolon ;

```
CREATE TABLE table_name (
   column_1 data_type, 
   column_2 data_type, 
   column_3 data_type
);
```

- CREATE TABLE is a clause. Clauses perform specific tasks in SQL. By convention, clauses are written in capital letters. Clauses can also be referred to as commands.
- table_name refers to the name of the table that the command is applied to.
- (column_1 data_type, column_2 data_type, column_3 data_type) is a parameter. A parameter is a list of columns, data types, or values that are passed to a clause as an argument. Here, the parameter is a list of column names and the associated data type.
<hr>

### CREATE
CREATE statements allow us to create a new table in the database. You can use the CREATE statement anytime you want to create a new table from scratch.
```
CREATE TABLE celebs (
   id INTEGER, 
   name TEXT, 
   age INTEGER
);
```
<hr>

### INSERT
The INSERT statement inserts a new row into a table.

We can use the INSERT statement when you want to add new records.
```
INSERT INTO celebs (id, name, age) 
VALUES (1, 'Craig Federighi', 53);
```
INSERT INTO is a clause that adds the specified row or rows. 
<hr>

### SELECT
SELECT statements are used to fetch data from a database. In the statement below, SELECT returns all data in the name column of the celebs table.
```
SELECT name FROM celebs;
```
SELECT is a clause that indicates that the statement is a query. You will use SELECT every time you query data from a database. 
<hr>

### ALTER
The ALTER TABLE statement adds a new column to a table. You can use this command when you want to add columns to a table. 
```
ALTER TABLE celebs 
ADD COLUMN twitter_handle TEXT;
```
<hr>

### UPDATE
The UPDATE statement edits a row in a table. You can use the UPDATE statement when you want to change existing records.
```
UPDATE celebs 
SET twitter_handle = '@wesbos' 
WHERE id = 4; 
```
WHERE is a clause that indicates which row(s) to update with the new column value.
<hr>

### DELETE
The DELETE FROM statement deletes one or more rows from a table. You can use the statement when you want to delete existing records.
```
DELETE FROM celebs 
WHERE twitter_handle IS NULL;
```
<hr>

### Constrains
Constraints that add information about how a column can be used are invoked after specifying the data type for a column. They can be used to tell the database to reject inserted data that does not adhere to a certain restriction.
```
CREATE TABLE celebs (
   id INTEGER PRIMARY KEY, 
   name TEXT UNIQUE,
   date_of_birth TEXT NOT NULL,
   date_of_death TEXT DEFAULT 'Not Applicable'
);
```
- PRIMARY KEY columns can be used to uniquely identify the row. Attempts to insert a row with an identical value to a row already in the table will result in a constraint violation which will not allow you to insert the new row.

- UNIQUE columns have a different value for every row. This is similar to PRIMARY KEY except a table can have many different UNIQUE columns.

- NOT NULL columns must have a value. Attempts to insert a row without a value for a NOT NULL column will result in a constraint violation and the new row will not be inserted.

- DEFAULT columns take an additional argument that will be the assumed value for an inserted row if the new row does not specify a value for that column.
<hr>

## To sum up:
SQL is a programming language designed to manipulate and manage data stored in relational databases.

A relational database is a database that organizes information into one or more tables.
A table is a collection of data organized into rows and columns.
A statement is a string of characters that the database recognizes as a valid command.

- CREATE TABLE creates a new table.
- INSERT INTO adds a new row to a table.
- SELECT queries data from a table.
- ALTER TABLE changes an existing table.
- UPDATE edits a row in a table.
- DELETE FROM deletes rows from a table.
- Constraints add information about how a column can be used.

# Queries
One of the core purposes of the SQL language is to retrieve information stored in a database. This is commonly referred to as querying. Queries allow us to communicate with the database by asking questions and returning a result set with data relevant to the question.

### Selecting only needed columns
```
SELECT name, genre 
FROM movies;
```
<hr>

## AS
AS is a keyword in SQL that allows you to rename a column or table using an alias. The new name can be anything you want as long as you put it inside of single quotes. Here we renamed the name column as Titles.

```
SELECT name AS 'Titles'
FROM movies;
```

Some important things to note:
- Although it’s not always necessary, it’s best practice to surround your aliases with single quotes.
- When using AS, the columns are not being renamed in the table. The aliases only appear in the result.
<hr>

## DISTINCT
DISTINCT is used to return unique values in the output. It filters out all duplicate values in the specified column(s).
```
SELECT DISTINCT tools 
FROM inventory;
```
<hr>

## WHERE
We can restrict our query results using the WHERE clause in order to obtain only the information we want.
```
SELECT *
FROM movies
WHERE imdb_rating > 8;
```
Comparison operators used with the WHERE clause are:
- = equal to
- != not equal to
- <p>> greater than</p>
- < less than
- <p>>= greater than or equal to</p>
- <= less than or equal to

<hr>

## LIKE
LIKE can be a useful operator when you want to compare similar values.
Let's imagine that a table contains two films with similar titles, ‘Se7en’ and ‘Seven’.
To select it, we need a query shown in the example below:
```
SELECT * 
FROM movies
WHERE name LIKE 'Se_en';
```
- LIKE is a special operator used with the WHERE clause to search for a specific pattern in a column.
- name LIKE 'Se_en' is a condition evaluating the name column for a specific pattern.
- Se_en represents a pattern with a wildcard character.

The _ means you can substitute any individual character here without breaking the pattern. The names Seven and Se7en both match this pattern.

The percentage sign % is another wildcard character that can be used with LIKE.

This statement below filters the result set to only include movies with names that begin with the letter ‘A’:
```
SELECT * 
FROM movies
WHERE name LIKE 'A%';
```
% is a wildcard character that matches zero or more missing letters in the pattern. For example:
- A% matches all movies with names that begin with letter ‘A’
- %a matches all movies that end with ‘a’

We can also use % both before and after a pattern:
```
SELECT * 
FROM movies 
WHERE name LIKE '%man%';
```
> **Note**
> <br>LIKE is not case sensitive. ‘Batman’ and ‘Man of Steel’ will both appear in the result of the query above.

Edit the query so that it selects all the information about the movie titles that begin with the word ‘The’.
```
SELECT * 
FROM movies
WHERE name LIKE 'The %';
```
<hr>

## NULL
Unknown values are indicated by NULL.
It is not possible to test for NULL values with comparison operators, such as = and !=.

Instead, we will have to use these operators:
- IS NULL
- IS NOT NULL

```
SELECT name
FROM movies 
WHERE imdb_rating IS NOT NULL;
```
<hr>

## BETWEEN
The BETWEEN operator is used in a WHERE clause to filter the result set within a certain range. It accepts two values that are either numbers, text or dates.
```
SELECT *
FROM movies
WHERE year BETWEEN 1990 AND 1999;
```
When the values are text, BETWEEN filters the result set for within the alphabetical range.
```
SELECT *
FROM movies
WHERE name BETWEEN 'A' AND 'J';
```
```
SELECT * 
FROM movies
WHERE year BETWEEN 1990 AND 1999
AND genre = 'romance';
```
Example with OR operator: 
```
SELECT *
FROM movies
WHERE year > 2014
OR genre = 'action';
```

<hr>

## ORDER BY
We can sort the results using ORDER BY, either alphabetically or numerically. Sorting the results often makes the data more useful and easier to analyze.
```
SELECT *
FROM movies
ORDER BY name;
```
Sometimes we want to sort things in a decreasing order.
```
SELECT *
FROM movies
WHERE imdb_rating > 8
ORDER BY year DESC;
```

- DESC is a keyword used in ORDER BY to sort the results in descending order (high to low or Z-A).
- ASC is a keyword used in ORDER BY to sort the results in ascending order (low to high or A-Z).

> **Note**
> <br>ORDER BY always goes after WHERE (if WHERE is present).

<hr>

## LIMIT
Most SQL tables contain hundreds of thousands of records. In those situations, it becomes important to cap the number of rows in the result.
For instance, imagine that we just want to see a few examples of records.
```
SELECT *
FROM movies
LIMIT 10;
```
```
SELECT *
FROM movies
ORDER BY imdb_rating DESC
LIMIT 3;
```
<hr>

## CASE
A CASE statement allows us to create different outputs (usually in the SELECT statement). It is SQL’s way of handling if-then logic.
Suppose we want to condense the ratings in movies to three levels:
- If the rating is above 8, then it is Fantastic.
- If the rating is above 6, then it is Poorly Received.
- Else, Avoid at All Costs.

```
SELECT name,
 CASE
  WHEN imdb_rating > 8 THEN 'Fantastic'
  WHEN imdb_rating > 6 THEN 'Poorly Received'
  ELSE 'Avoid at All Costs'
 END
FROM movies;
```
In the result, you have to scroll right because the column name is very long. To shorten it, we can rename the column to ‘Review’ using AS:
```
SELECT name,
 CASE
  WHEN imdb_rating > 8 THEN 'Fantastic'
  WHEN imdb_rating > 6 THEN 'Poorly Received'
  ELSE 'Avoid at All Costs'
 END AS 'Review'
FROM movies;
```

<hr>

## Let’s summarize:

- SELECT is the clause we use every time we want to query information from a database.
- AS renames a column or table.
- DISTINCT return unique values.
- WHERE is a popular command that lets you filter the results of the query based on conditions that you specify.
- LIKE and BETWEEN are special operators.
- AND and OR combines multiple conditions.
- ORDER BY sorts the result.
- LIMIT specifies the maximum number of rows that the query will return.
- CASE creates different outputs.
