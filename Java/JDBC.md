# JDBC Overview

### What is JDBC?

JDBC refers to the Java Database Connectivity. It provides java API that allows Java programs to access database management systems (relational database). The JDBC API consists of a set of interfaces and classes which enables java programs to execute SQL statements. Interfaces and classes in JDBC API are written in java.

### JDBC core components:

**The JDBC API consists of the following core components:**
1. JDBC Drivers
2. Connections
3. Statements
4. ResultSets

** **

**1. JDBC Drivers:**

JDBC driver is a collection of classes which implements interfaces defined in the JDBC API for opening database connections, interacting with database and closing database connections.

**2. Connections:**

Before performing any database operation via JDBC, we have to open a database connection. To open a database connection we can call getConnection() method of DriverManager class.

```java
Connection connection = DriverManager.getConnection(url, user, password) 
```

**3. Statements:**

The JDBC statements are used to execute the SQL or PL/SQL queries against the database. We need a statement for every single query. JDBC API defines the _Statement_, _CallableStatement_, and _PreparedStatement_ types of statements.

**4. ResultSets:**

A query returns the data in the form of ResultSet. To read the query result date ResultSet provides a cursor that points to the current row in the result set.


## JDBC driver

#### Driver:
A driver is a software component that provides the facility to a computer to communicate with hardware.

### JDBC driver:

A driver is a software component that provides the facility to interact java application with the database.

#### Types of JDBC drivers:
1. JDBC-ODBC bridge driver.
2. Native-API driver.
3. Network-Protocol driver.
4. Thin driver.

### 1. JDBC-ODBC bridge driver:

JDBC-ODBC bridge driver is a native code driver which uses ODBC driver to connect with the database. It converts JDBC method calls into ODBC function calls. It is also known as Type 1 driver.

**Advantages:**
1. It can be used with any database for which an ODBC driver is installed.

**Disadvantages:**
1. Performance is not good as it converts JDBC method calls into ODBC function calls.
2. ODBC driver needs to be installed on the client machine.
3. Platform dependent.

### 2. Native-API driver:

Native-API driver uses the client-side libraries of the database. It converts JDBC method calls into native calls of the database API. It is partially written in java. It is also known as Type 2 driver.

**Advantages:**
1. It is faster than a JDBC-ODBC bridge driver.

**Disadvantages:**
1. Platform dependent.
2. The vendor client library needs to be installed on the client machine.

### 3. Network-Protocol driver:

Network-Protocol driver is a pure java driver which uses a middle-tier to converts JDBC calls directly or indirectly into database specific calls. Multiple types of databases can be accessed at the same time. It is a platform independent driver. It is also known as Type 3 or MiddleWare driver.

**Advantages:**
1. Platform independent.
2. Faster from Type1 and Type2 drivers.
3. It follows a three tier communication approach.
4. Multiple types of databases can be accessed at the same time.

**Disadvantages:**
1. It requires database-specific coding to be done in the middle tier.

### 4. Thin driver:

Thin driver is a pure java driver which converts JDBC calls directly into the database specific calls. It is a platform independent driver. It is also known as Type 4 or Database-Protocol driver.

**Advantages:**
1. Platform independent.
2. Faster than all other drivers.

**Disadvantages:**
1. It is database dependent.
2. Multiple types of databases can’t be accessed at the same time.

























