---
date: 2021-05-23
title: Creating and Dropping Tables
categories:
  - databases
description: How to create and drop tables using SQL
type: Document
order_number: 2
---
## Creating Tables

```
CREATE TABLE table_name(
  column1 datatype constraint,
  column2 datatype constraint,
  ...
)
```

## Data Types
[Click here to see all the data types](https://www.w3schools.com/sql/sql_datatypes.asp)

## Constraints
* NOT NULL - Ensures that a column cannot have a NULL value
* UNIQUE - Ensures that all values in a column are different
* PRIMARY KEY - A combination of a NOT NULL and UNIQUE. Uniquely identifies each row in a table
* FOREIGN KEY - Prevents actions that would destroy links between tables
* CHECK - Ensures that the values in a column satisfies a specific condition
* DEFAULT - Sets a default value for a column if no value is specified
* CREATE INDEX - Used to create and retrieve data from the database very quickly

## Dropping Tables

`DROP TABLE table_name`