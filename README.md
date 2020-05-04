# SQL Cheat Sheet

## Introduction

My experience with using SQL often occurs in chunks, when setting up a database and then implementing any new features. It is a language I always end up searching for the exact syntax after not having used for a while, therefore I thought it would be useful to produce this document to improve my understanding of the language, but also to be used as a reference whenever I need to re-visit SQL. I use MySQL syntax and have included links to the web pages for more information.

## Table of Contents

1. [Database](#Database)
   1. [Database Creation](#Database-Creation)
   2. [Database Deletion](#Database-Delection)
2. [Table](#Table)
   1. [Table Creation](#Table-Creation)
   2. [Table Deletion](#Table-Deletion)
   3. [Table Modification](#Table-Modification)
      1. [Add Column](#Add-Column)
      2. [Remove Column](#Remove-Column)
      3. [Modify Column](#Modify-COlumn)
3. [Querying](#Querying)
   1. [Statements](#Statements)
      1. [Select](#Select)
      2. [Insert](#Insert)
      3. [Update](#Update)
      4. [Delete](#Delete)
   2. [Conditions](#Conditions)
      1. [And](#And)
      2. [OR](#OR)
      3. [NOT](#NOT)
      4. [Parenthesis](#Parenthesis)
4. [Data Types](#Data-Types)
   1. [String](#String)
   2. [Integer](#Integer)
   3. [Floating Point](#Floating-Point)
   4. [Fixed Point](#Fixed-Point)
   5. [JSON](#JSON)
   6. [Time](#Time)
5. [Relational Databases](#Relational-Databases)
   1. [Primary Key](#Primary-Key)
   2. [Foreign Key](#Foreign-Key)

## Database

### [Database Creation](https://dev.mysql.com/doc/refman/5.7/en/create-database.html)

```mysql
CREATE DATABASE dbname;
```

### [Database Deletion](https://dev.mysql.com/doc/refman/5.7/en/drop-database.html)

```mysql
DROP DATABASE dbname;
```

## Table

### [Table Creation](https://dev.mysql.com/doc/refman/5.7/en/create-table.html)

```mysql
CREATE TABLE TableName (
    colName1 type,
    colName2 type,
    colName3 type
);
```

### [Table Deletion](https://dev.mysql.com/doc/refman/5.7/en/drop-table.html)

```mysql
DROP TABLE TableName;
```

### [Table Modification](https://dev.mysql.com/doc/refman/5.7/en/alter-table.html)

#### Add Column

```mysql
ALTER TABLE TableName
ADD colName type;
```

#### Remove Column

```mysql
ALTER TABLE TableName
DROP colName;
```

#### Modify Column

```mysql
ALTER TABLE TableName
MODIFY COLUMN colName newType;
```

## Querying

### Statements

#### [Select](https://dev.mysql.com/doc/refman/5.7/en/select.html)

```mysql
SELECT colName1, colName2, ...
FROM TableName
WHERE {condition}
ORDER BY colName1 [ASC|DESC];
```

#### [Insert](https://dev.mysql.com/doc/refman/5.7/en/insert.html)

```mysql
INSERT INTO TableName (colName1, colName2, ...)
VALUES (value1, value2, ...);
```

#### [Update](https://dev.mysql.com/doc/refman/5.7/en/update.html)

```mysql
UPDATE TableName
SET colName1 = value1, colName2 = value2, ...
WHERE {condition};
```

#### [Delete](https://dev.mysql.com/doc/refman/5.7/en/delete.html)

```mysql
DELETE FROM TableName
WHERE {condition};
```

### Conditions

#### And

```mysql
condition1 AND condition2
```

#### OR

```mysql
condition1 OR condition2
```

#### NOT

```mysql
NOT condition1
```

#### Parenthesis

```mysql
NOT ( (condition1 OR condition2) AND NOT (condition3 AND condition4) )
```

## [Data Types](https://dev.mysql.com/doc/refman/5.7/en/data-types.html)

### [String](https://dev.mysql.com/doc/refman/5.7/en/string-type-syntax.html)

Length defines the maximum number of characters in the string

```mysql
VARCHAR(length)
```

### [Integer](https://dev.mysql.com/doc/refman/5.7/en/integer-types.html)

Just a normal integer

```mysql
INT
```

### [Floating Point](https://dev.mysql.com/doc/refman/5.7/en/floating-point-types.html)

Used when approximate values can be recorded

```mysql
FLOAT
```

```mysql
DOUBLE
```

### [Fixed Point](https://dev.mysql.com/doc/refman/5.7/en/fixed-point-types.html)

Used when exact values must be recorded. `precision` is number of digits to be stored and `scale` is the number of digits can be stored after the decimal point.

```mysql
DECIMAL(precision, scale)
```

### [Time](https://dev.mysql.com/doc/refman/5.7/en/date-and-time-type-syntax.html)

`YYYY-MM-DD`

```mysql
DATE
```

`YYYY-MM-DD hh:mm:ss[.fraction]`

```mysql
DATETIME
```

Number of seconds since the epoch (1970-01-01 00:00:00 UTC)

```mysql
TIMESTAMP
```

### [JSON](https://dev.mysql.com/doc/refman/5.7/en/json.html)

Stores JSON objects as strings, but provides validation and optimises storage

```mysql
JSON
```

## Relational Databases

This type of database allows records to be *related* to records from other tables. When you have multiple tables, each serving a different purpose to keep data organised, you may want to have one unique identifier which you can trace throughout the database to find all information storge about one entity e.g. user or process.

### [Primary Key](#Primary-Key)

Unique identifier for the record. There cannot be another record with this value within the same column of a table. The following code creates a table with `id` as the primary key. `NOT NULL` ensures this column requires a value when a record is inserted. `AUTO_INCREMENT` starts at 1 and increments each time a new record is added. 

```mysql
CREATE TABLE Users (
    user_id INT NOT NULL AUTO_INCREMENT,
    username VARCHAR(15),
    age INT,
    PRIMARY KEY (user_id)
); 
```

### [Foreign Key](#Foreign-Key)

Links two tables together. A `FOREIGN KEY` in one table must be a `Primary Key` in another table.

```mysql
CREATE TABLE Messages (
    message_id INT NOT NULL AUTO_INCREMENT,
    user_id INT NOT NULL,
    text VARCHAR(255),
    time_send TIMESTAMP,
    PRIMARY KEY (message_id),
    FOREIGN KEY (user_id) REFERENCES Users(user_id)
); 
```
