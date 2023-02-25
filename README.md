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
