# JDBC Overview

### What is JDBC?

JDBC refers to the Java Database Connectivity. It provides java API that allows Java programs to access database management systems (relational database). The JDBC API consists of a set of interfaces and classes which enables java programs to execute SQL statements. Interfaces and classes in JDBC API are written in java.

### JDBC core components:

**The JDBC API consists of the following core components:**
1. JDBC Drivers
2. Connections
3. Statements
4. ResultSets

1. JDBC Drivers:

JDBC driver is a collection of classes which implements interfaces defined in the JDBC API for opening database connections, interacting with database and closing database connections.

2. Connections:

Before performing any database operation via JDBC, we have to open a database connection. To open a database connection we can call getConnection() method of DriverManager class.

```java
Connection connection = DriverManager.getConnection(url, user, password) 
```

3. Statements:

The JDBC statements are used to execute the SQL or PL/SQL queries against the database. We need a statement for every single query. JDBC API defines the Statement, CallableStatement, and PreparedStatement types of statements.

4. ResultSets:

A query returns the data in the form of ResultSet. To read the query result date ResultSet provides a cursor that points to the current row in the result set.
