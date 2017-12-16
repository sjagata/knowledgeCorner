### 1. What is DBMS?
A Database Management System (DBMS) is a program that controls creation, maintenance and use of a database. DBMS can be termed as File Manager that manages data in a database rather than saving it in file systems.

### 2. What is RDBMS?
RDBMS stands for Relational Database Management System. RDBMS store the data into the collection of tables, which is related by common fields between the columns of the table. It also provides relational operators to manipulate the data stored into the tables.<br>
Example: Mysql, SQL Server.

**The key difference is that RDBMS (relational database management system) applications store data in a tabular form, while DBMS applications store data as files.**

Does that mean there are no tables in a DBMS?

There can be, but there will be no “relation” between the tables, like in a RDBMS. In DBMS, data is generally stored in either a hierarchical form or a navigational form. This means that a single data unit will have one parent node and zero, one or more children nodes. It may even be stored in a graph form, which can be seen in the network model.

In a RDBMS, the tables will have an identifier called **primary key**. Data values will be stored in the form of tables. The relationships between these data values will be stored in the form of a table as well. Every value stored in the relational database is accessible. This value can be updated by the system. The data in this system is also physically and logically independent.

You can say that a RDBMS is an extension of a DBMS, even if there are many differences between the two. Most software products in the market today are both DBMS and RDBMS compliant. Essentially, they can maintain databases in a (relational) tabular form as well as a file form, or both. This means that today a RDBMS application is a DBMS application, and vice versa. However, there are still major differences between a relational database system for storing data and a plain database system. <br>
[source](https://stackoverflow.com/questions/18419137/what-is-the-difference-between-dbms-and-rdbms)


### 3. What is SQL?
SQL stands for Structured Query Language , and it is used to communicate with the Database. This is a standard language used to perform tasks such as retrieval, updation, insertion and deletion of data from a database.<br>
Standard SQL Commands are Select.

### 4. What is a Database?
Database is nothing but an organized form of data for easy access, storing, retrieval and managing of data. This is also known as structured form of data which can be accessed in many ways. <br>
Example: School Management Database, Bank Management Database.

### 5. What are tables and Fields?
A table is a set of data that are organized in a model with Columns and Rows. Columns can be categorized as vertical, and Rows are horizontal. A table has specified number of column called fields but can have any number of rows which is called record.

### 6. What is a primary key?
A primary key is a combination of fields which uniquely specify a row. This is a special kind of unique key, and it has implicit NOT NULL constraint. It means, Primary key values cannot be NULL.

### 7. What is a unique key?
A Unique key constraint uniquely identified each record in the database. This provides uniqueness for the column or set of columns.
* A Primary key constraint has automatic unique constraint defined on it. But not, in the case of Unique Key.
* There can be many unique constraint defined per table, but only one Primary key constraint defined per table.

### 8. What is a foreign key?
A foreign key is one table which can be related to the primary key of another table. Relationship needs to be created between two tables by referencing foreign key with the primary key of another table.

### 9. What is a join?
This is a keyword used to query data from more tables based on the relationship between the fields of the tables. Keys play a major role when JOINs are used.

### 10. What are the types of join and explain each?
There are various types of join which can be used to retrieve data and it depends on the relationship between tables.
* Inner join.
Inner join return rows when there is at least one match of rows between the tables.
* Right Join.
Right join return rows which are common between the tables and all rows of Right hand side table. Simply, it returns all the rows from the right hand side table even though there are no matches in the left hand side table.
* Left Join.
Left join return rows which are common between the tables and all rows of Left hand side table. Simply, it returns all the rows from Left hand side table even though there are no matches in the Right hand side table.
* Full Join.
Full join return rows when there are matching rows in any one of the tables. This means, it returns all the rows from the left hand side table and all the rows from the right hand side table.








<br>
<br>

References:
* [link](https://career.guru99.com/top-50-sql-question-answers/)
