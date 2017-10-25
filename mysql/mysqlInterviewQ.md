### Compare MySQL Vs. SQL Server

MySQL
* Targeted towards : Internet servers & Open Source software
* Functionality : Speed
* Works with : Assumes internet access

SQL
* Targeted towards : Corporate & Enterprise market
* Functionality : Administration, Graphical data modelling
* Works with : Administration, Graphical data modelling

<br>
<br>

### What is SQL Server?
SQL Server is   one of the Database Management Systems (DBMS) and is designed by Microsoft.  DBMS are computer software applications with the capability of interacting with user, various other applications as well as the database itself. The objective is capturing and analyzing data and manages definition, querying, creation, updating as well as administration of database.

<br>
<br>

### How and why use it?
SQL Server is free and anyone can download and use it. The application uses SQL (Structured Query Language) and is easy to use.

<br>
<br>

### What are the features of MySQL?
MySQL provides cross-platform support, wide range of interfaces for application programming and has many stored procedures like triggers and cursors that helps in managing the database.

<br>
<br>

### What do DDL, DML, and DCL stand for?
**DDL** is the abbreviation for **Data Definition Language** dealing with database schemas as well as the description of how data resides in the database. An example is **CREATE TABLE** command. **DML** denotes **Data Manipulation Language** such as **SELECT, INSERT** etc. **DCL** stands for **Data Control Language** and includes commands like **GRANT, REVOKE** etc.

<br>
<br>

### What are meant by Joins in MySQL?
In MySQL the Joins are used to **query data from two or more tables.** The query is made using relationship between certain columns existing in the table. There are four types of Joins in MySQL. Inner Join returns the rows if there is at least one match in both the tables. Left Join returns all the rows form the left table even if there is no match in the right table. Right Join returns all the rows from the right table even if no matches exist in left table. Full Join would return rows when there is at least one match in the tables.

<br>
<br>

### What are the common MySQL functions?
* **NOWO** – function for returning current date and time as single value. 
* **CURRDATEO** – function for returning the current date or time. 
* **CONCAT (X, Y)** – function to concatenates two string values creating single string output. 
* **DATEDIFF (X, Y)** – function to determine difference two dates.

<br>
<br>

### What is the difference between CHAR and VARCHAR?
When the table is created, **CHAR** is used to define the fixed length of the table and columns. The length value could be in the range of 1-255. **VARCHAR** command is given to adjust the column and table length as required.

<br>
<br>

### What are the different types of strings in Database columns in MySQL?
Different types of strings that can be used for database columns are SET, BLOB, VARCHAR, TEX, ENUM, and CHAR.

<br>
<br>

### What is the difference between primary key and candidate key?
**Primary key** in MySQL is use to identify every row of a table in unique manner. For one table there is only one primary key. One of the **candidate keys** is the primary key and the candidate keys can be **used to reference the foreign keys.**

<br>
<br>

### What are the TRIGGERS that can be used in MySQL tables?
The following TRIGGERS are allowed in MySQL:
* BEFORE INSERT
* AFTER INSERT
* BEFORE UPDATE
* AFTER UPDATE
* BEFORE DELETE
* AFTER DELETE

<br>
<br>

### What is the difference between LIKE and REGEXP operators in MySQL?
* **LIKE is denoted using the % sign.**
For example:

```sql
SELECT * FROM user WHERE user name LIKE “%NAME”.
```
*  On the other hand the use of REGEXP is as follows:

```sql
SELECT * FROM user WHERE username REGEXP “^NAME”;
```
<br>
<br>

### What is the difference between DELETE TABLE and TRUNCATE TABLE commands in MySQL?
Basically DELETE TABLE is logged operation and every row deleted is logged. Therefore the process is usually slow. TRUNCATE TABLE also deletes rows in a table but it will not log any of the rows deleted.  The process is faster in comparison. TRUNCATE TABLE can be rolled back and is functionally similar to the DELETE statement using no WHERE clause.v









