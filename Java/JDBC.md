# JDBC Overview

### What is JDBC?

JDBC refers to the Java Database Connectivity. It provides java API that allows Java programs to access database management systems (relational database). The JDBC API consists of a set of interfaces and classes which enables java programs to execute SQL statements. Interfaces and classes in JDBC API are written in java.

### JDBC core components:

**The JDBC API consists of the following core components:**
1. JDBC Drivers
2. Connections
3. Statements
4. ResultSets

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

** **

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


** **

## Connect to Oracle database with JDBC driver

To connect with oracle database with JDBC driver follow the same basic steps discussed in previous tutorials. We have to know the following information to connect with oracle database:
1. **Driver class:** oracle.jdbc.driver.OracleDriver.
2. **Connection URL:**

```java
“jdbc:oracle:thin:@localhost:port:serviceName”,”username”, “password”.
```

**Connection url for MySql database:**
```java
jdbc:oracle:thin:@localhost:1521:xe

//where 1521 is the port number and XE is the Oracle service name.
```

3. **Username:** Username of oracle database, default is system.
4. **Password:** Password of oracle database.

### Example

```java

// JDBCOracleTest.java

package jdbc;

import java.sql.Connection;
import java.sql.DriverManager;

public class JDBCOracleTest {
	// JDBC and database properties.
	private static final String DB_DRIVER = "oracle.jdbc.driver.OracleDriver";
	private static final String DB_URL = "jdbc:oracle:thin:@localhost:1521:XE";
	private static final String DB_USERNAME = "system";
	private static final String DB_PASSWORD = "oracle";

	public static void main(String args[]) {
		Connection conn = null;
		try {
			// Register the JDBC driver
			Class.forName(DB_DRIVER);

			// Open the connection
			conn = DriverManager.getConnection(DB_URL, DB_USERNAME, DB_PASSWORD);

			if (conn != null) {
				System.out.println("Successfully connected.");
			} else {
				System.out.println("Failed to connect.");
			}
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}

```


## Connect to MySql database with JDBC driver

To connect with MySql database with JDBC driver follow the same basic steps discussed in previous tutorials. We have to know the following information to connect with mysql database:

1. **Driver class:** com.mysql.jdbc.Driver.
2. **Connection URL:**

```java
“jdbc:mysql://hostname:port/dbname”,”username”, “password”.

//Connection url for MySql database: 
jdbc:mysql://localhost:3306/javawithease

//where 3306 is the port number and javawithease is the database name.
```

3. **Username:** Username of MySql database, default is root.
4. **Password:** Password of MySql database.

### Example:

```java

// JDBCMySqlTest.java

package jdbc;

import java.sql.Connection;
import java.sql.DriverManager;

public class JDBCMySqlTest {
	// JDBC and database properties.
	private static final String DB_DRIVER = "com.mysql.jdbc.Driver";
	private static final String DB_URL = "jdbc:mysql://localhost:3306/javawithease";
	private static final String DB_USERNAME = "root";
	private static final String DB_PASSWORD = "root";

	public static void main(String args[]) {
		Connection conn = null;
		try {
			// Register the JDBC driver
			Class.forName(DB_DRIVER);

			// Open the connection
			conn = DriverManager.getConnection(DB_URL, DB_USERNAME, DB_PASSWORD);

			if (conn != null) {
				System.out.println("Successfully connected.");
			} else {
				System.out.println("Failed to connect.");
			}
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}


```


** **


## JDBC Statement interface

The JDBC statement is used to execute queries against the database. Statement is an interface which provides the methods to execute queries. We can get a statement object by invoking the createStatement() method of Connection interface.

```java
Statement stmt=conn.createStatement();
```

### Commonly used methods of Statement interface:

**1. execute(String SQL):** 
It is used to execute SQL DDL statements.

```java
public boolean execute(String SQL)
```

**2. executeQuery(String SQL):**
It is used to execute the select query and returns an object of ResultSet.

```java
public ResultSet executeQuery(String SQL)
```

**3. executeUpdate(String SQL):**
It is used to execute the query like inset, update, delete etc. It returns the no. of affected rows.

```java
public int executeUpdate(String SQL)
```

**4. executeBatch():**
It is used to execute the batch of commands.

```java
public int[] executeBatch()
```

** **

## JDBC PreparedStatement interface

The JDBC PreparedStatement is used to execute parameterized queries against the database. PreparedStatement is an interface which provides the methods to execute parameterized queries. A parameter is represented by ? symbol in JDBC. PreparedStatement extends the Statement interface. We can get a PreparedStatement object by invoking the prepareStatement() method of Connection interface.

```java
PreparedStatement pstmt = conn.prepareStatement(SQL);
```

**Advantages of PreparedStatement:**
1. **Parameterized query:** Provides the facility of parameterized query.
2. **Reusable:** PreparedStatement can be easily used with new parameters.
3. **Performance:** It increases the performance because of database statement caching.

### Difference between Statement and PreparedStatement in jdbc:
|Statement|PreparedStatement|
| --------|-----------------|
| 1. Statement not executes the parameterized query.| 1. PreparedStatement can execute the parameterized query.| 
| 2. Relational DB uses following 4 step to execute a query:| 2. Relational DB uses following 4 step to execute a query:| 
| a. Parse the query.| a. Parse the query.| 
| b. Compile the query.| | 
| c. Optimize/Plan the query.| | 
| d. Execute the query.| | 
| A statement always executes the all four steps.| | 
| 3. No database statement caching in case of statement.| | 


<table>
  <tr>
    <td>Statement</td>
    <td>PreparedStatement</td>
  </tr>
  <tr>
    <td> 1. Statement not executes the parameterized query</td>
    <td> 1. PreparedStatement can execute the parameterized query.</td>
  </tr>
  <tr>
    <td> 2. Relational DB uses following 4 step to execute a query:
    * Parse the query.
    * Compile the query.
    * Optimize/Plan the query.
    * Execute the query. `A statement always executes the all four steps.`
    </td>
    <td> 2. Relational DB uses following 4 step to execute a query:
    * Parse the query.
    * Compile the query.
    * Optimize/Plan the query.
    * Execute the query. `PreparedStatement pre-executes first three steps in the execution.`
    </td>
  </tr>
  <tr>
  <td>3. No database statement caching in case of statement.</td>
  <td>3. It provides the database statement caching the execution plans of previously executed statements. Hence database engine can reuse the plans for statements that have been executed previously.</td>
  </tr>
</table>


a. Parse the query.
b. Compile the query.
c. Optimize/Plan the query.
d. Execute the query.
PreparedStatement pre-executes first three steps in the execution.
3. It provides the database statement caching the execution plans of previously executed statements. Hence database engine can reuse the plans for statements that have been executed previously.






















** **

# Examples :

** **

### JDBC Statement creates a table example

The JDBC statement is used to execute queries against the database. Let us study JDBC Statement by create table example.

#### Example

```java

// JDBCCreateTest.java

package jdbc;

import java.sql.Connection;
import java.sql.Statement;

/**
 * This class is used to create a table in DB.
 */
public class JDBCCreateTest {
	public static void main(String args[]) {
		Connection conn = null;
		Statement statement = null;

		String query = "create table EMPLOYEE(" + "EMPLOYEE_ID NUMBER(5) NOT NULL, " + "NAME VARCHAR(20) NOT NULL, "
				+ "SALARY NUMBER(10) NOT NULL, " + "PRIMARY KEY (EMPLOYEE_ID) )";

		try {
			// get connection
			conn = JDBCUtil.getConnection();

			// create statement
			statement = conn.createStatement();

			// execute query
			statement.execute(query);

			// close connection
			statement.close();
			conn.close();

			System.out.println("Table created successfully.");
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}

```

```java

// JDBCUtil.java

package jdbc;

import java.sql.Connection;
import java.sql.DriverManager;

/**
 * This is a utility class for JDBC connection.
 */
public class JDBCUtil {
	// JDBC and database properties.
	private static final String DB_DRIVER = "oracle.jdbc.driver.OracleDriver";
	private static final String DB_URL = "jdbc:oracle:thin:@localhost:1521:XE";
	private static final String DB_USERNAME = "system";
	private static final String DB_PASSWORD = "oracle";

	public static Connection getConnection() {
		Connection conn = null;
		try {
			// Register the JDBC driver
			Class.forName(DB_DRIVER);

			// Open the connection
			conn = DriverManager.getConnection(DB_URL, DB_USERNAME, DB_PASSWORD);

			if (conn != null) {
				System.out.println("Successfully connected.");
			} else {
				System.out.println("Failed to connect.");
			}
		} catch (Exception e) {
			e.printStackTrace();
		}
		return conn;
	}
}
```

### JDBC Statement inserts a record example
JDBC Statement inserts a record example

#### Example

```java

// JDBCInsertTest.java

package jdbc;

import java.sql.Connection;
import java.sql.Statement;

public class JDBCInsertTest {
	public static void main(String args[]) {
		Connection conn = null;
		Statement statement = null;

		String query = "insert into EMPLOYEE " + "(EMPLOYEE_ID, NAME, SALARY) " + "values (1, 'Jhon Doe', 85000)";

		try {
			// get connection
			conn = JDBCUtil.getConnection();

			// create statement
			statement = conn.createStatement();

			// execute query
			statement.executeUpdate(query);

			// close connection
			statement.close();
			conn.close();

			System.out.println("Record inserted successfully.");
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}

```

### JDBC Statement updates a record example

The JDBC statement is used to execute queries against the database. Let us study JDBC Statement by update a record example.

#### Example

```java

// JDBCUpdateTest.java

package jdbc;

import java.sql.Connection;
import java.sql.Statement;

public class JDBCUpdateTest {
	public static void main(String args[]) {
		Connection conn = null;
		Statement statement = null;

		String query = "update EMPLOYEE set " + "NAME = 'Jhon Doe' " + "where EMPLOYEE_ID = 1 ";

		try {
			// get connection
			conn = JDBCUtil.getConnection();

			// create statement
			statement = conn.createStatement();

			// execute query
			statement.executeUpdate(query);

			// close connection
			statement.close();
			conn.close();

			System.out.println("Record updated successfully.");
		} catch (Exception e) {
			e.printStackTrace();
		}
	}

}
```

### JDBC Statement select records example

The JDBC statement is used to execute queries against the database. Let us study JDBC Statement by select records example.

#### Example

```java
// JDBCSelectTest.java

package jdbc;

import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.Statement;

public class JDBCSelectTest {
	public static void main(String args[]) {
		Connection conn = null;
		Statement statement = null;

		String query = "select EMPLOYEE_ID, NAME from EMPLOYEE";

		try {
			// get connection
			conn = JDBCUtil.getConnection();

			// create statement
			statement = conn.createStatement();

			// execute query
			ResultSet rs = statement.executeQuery(query);
			while (rs.next()) {
				String empId = rs.getString("EMPLOYEE_ID");
				String empName = rs.getString("NAME");

				System.out.println("EmpId : " + empId);
				System.out.println("EmpName : " + empName);
			}

			// close connection
			statement.close();
			conn.close();
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}
```

### JDBC Statement deletes a record example
The JDBC statement is used to execute queries against the database. Let us study JDBC Statement by deletes a record example.

#### Example

```java

// JDBCDeleteTest.java

package jdbc;

import java.sql.Connection;
import java.sql.Statement;

/**
 * This class is used to delete a record from DB table.
 */

public class JDBCDeleteTest {
	public static void main(String args[]) {
		Connection conn = null;
		Statement statement = null;

		String query = "delete EMPLOYEE " + "where EMPLOYEE_ID = 1 ";

		try {
			// get connection
			conn = JDBCUtil.getConnection();

			// create statement
			statement = conn.createStatement();

			// execute query
			statement.executeUpdate(query);

			// close connection
			statement.close();
			conn.close();

			System.out.println("Record deleted successfully.");
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}
```

### JDBC Statement batch update example

The JDBC statement is used to execute queries against the database. Let us study JDBC Statement by batch update example.

#### Example

```java

// JDBCBatchTest.java

package jdbc;

import java.sql.Connection;
import java.sql.Statement;

/**
 * This class is used to batch update in DB table.
 */
public class JDBCBatchTest {
	public static void main(String args[]) {
		Connection conn = null;
		Statement statement = null;

		String query1 = "insert into EMPLOYEE " + "(EMPLOYEE_ID, NAME, SALARY) " + "values (1, 'Jane Doe', 50000)";

		String query2 = "insert into EMPLOYEE " + "(EMPLOYEE_ID, NAME, SALARY) " + "values (5, 'John Doe', 50000)";

		try {
			// get connection
			conn = JDBCUtil.getConnection();

			// create statement
			statement = conn.createStatement();

			// set auto commit to false
			conn.setAutoCommit(false);

			// add queries to batch
			statement.addBatch(query1);
			statement.addBatch(query2);

			// execute batch
			statement.executeBatch();

			// commit
			conn.commit();

			// close connection
			statement.close();
			conn.close();

			System.out.println("Records inserted successfully.");
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}

```















































