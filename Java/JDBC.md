# JDBC Overview

<br>

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

<br>
<br>

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

<br>
<br>

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

<br>
<br>

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

<br>
<br>

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
    <td> 2. Relational DB uses following 4 step to execute a <br> query: <br>
    * Parse the query.<br>
    * Compile the query.<br>
    * Optimize/Plan the query.<br>
    * Execute the query. <br><br>A statement always executes the all four steps.
    </td>
    <td> 2. Relational DB uses following 4 step to execute a <br> query:<br>
    * Parse the query.<br>
    * Compile the query.<br>
    * Optimize/Plan the query.<br>
    * Execute the query. <br><br> PreparedStatement pre-executes first three steps in the execution.
    </td>
  </tr>
  <tr>
  <td>3. No database statement caching in case of statement.</td>
  <td>3. It provides the database statement caching the execution plans of previously executed statements. <br> Hence database engine can reuse the plans for statements that have been executed previously.</td>
  </tr>
</table>

<br>
<br>

** **

## JDBC CallableStatement interface
The JDBC CallableStatement is used to execute the store procedure and functions. CallableStatement interface provides the methods to execute the store procedure and functions. We can get a statement object by invoking the prepareCall() method of Connection interface.

```java
CallableStatement callableStatement = conn.prepareCall(“{call procedurename(?,?…?)}”);
```

_**Note:** A store procedure is used to perform business logic and may return zero or more values. A function used to perform calculation and it can return only one value._

_**Note:** PreparedStatement can only use IN parameters. CallableStatement can use both IN and OUT parameters._

<br>
<br>

** **

## JDBC batch processing
The JDBC batch processing provides the facility to execute a group of related queries. A group of related queries is known as a batch. It reduces the amount of communication overhead and hence improves the performance.

### JDBC batch processing methods:

**1. addBatch(String query):**
It is used to add the statement to the batch.

```java
public void void addBatch(String query) throws SQLException
```

**2. executeBatch():**
It is used to execute batch.

```java
public int[] executeBatch() throws SQLException
```

**3. clearBatch():**
It is used to remove all statements from the batch.

```java
public void clearBatch() throws SQLException
```

<br>
<br>

** **

## JDBC store file example
PreparedStatement provides the facility to store and retrieve the file in the database using JDBC.

### PreparedStatement methods to store file:

```java
public void setCharacterStream(int paramIndex,InputStream stream) throws SQLException 
```

```java
public void setCharacterStream(int paramIndex,InputStream stream,long length) throws SQLException  
```

## JDBC retrieve file example
PreparedStatement provides the facility to store and retrieve the file in the database using JDBC.

### PreparedStatement methods to retrieve file:

```java
public Clob getClob(int columnIndex) throws SQLException
```

<br>
<br>

** **

## JDBC store image example
PreparedStatement provides the facility to store and retrieve the images in the database using JDBC.

### PreparedStatement methods to store image:

```java
public void setCharacterStream(int paramIndex, InputStream stream) throws SQLException 
```

```java
public void setCharacterStream(int paramIndex, InputStream stream, long length) throws SQLException  
```

## JDBC retrieve image example
PreparedStatement provides the facility to store and retrieve the file in the database using JDBC.

### PreparedStatement methods to retrieve image:

```java
public Blob getBlob(int columnIndex) throws SQLException 
```

<br>
<br>

** **

## JDBC ResultSetMetaData interface
The metadata refers to the data about data. The ResultSetMetaData interface provides the facility to get the information like table name, total number of column, column name and column type etc. We can get the object of ResultSetMetaData by calling getMetaData() method of ResultSet interface.

```java
ResultSetMetaData rsmd = resultSet.getMetaData();
```

### Commonly used methods of ResultSetMetaData:

**1. getTableName(int index):**
It returns the name of the table of the specified column index.

```java
public String getTableName(int index) throws SQLException
```

**2. getColumnCount():**
It returns the no. of columns in the result set.

```java
public int getColumnCount() throws SQLException
```

**3. getColumnName(int index):**
It returns the name of the column at the specified column index.

```java
public String getColumnName(int index) throws SQLException
```

**4. getColumnTypeName(int index):**
It returns the type of the column at the specified column index.

```java
public String getColumnTypeName(int index) throws SQLException
```



<br>
<br>

** **

## JDBC DatabaseMetaData interface
The metadata refers to the data about data. The DatabaseMetaData interface provides the facility to get the information like driver name, total number of tables and driver version etc. We can get the object of DatabaseMetaData by calling getMetaData() method of Connection interface.

```java
DatabaseMetaData dbmd=conn.getMetaData();
```

### Commonly used methods of DatabaseMetaData:

**1. getDriverName():**
It is used to get thename of the JDBC driver.

```java
public String getDriverName()throws SQLException
```

**2. getDriverVersion():**
 It is used to get the JDBC driver version.

```java
public String getDriverVersion()throws SQLException
```

**3. getUserName():**
 It is used to get the database username.

```java
public String getUserName()throws SQLException
```

**4. getDatabaseProductName():**
 It is used to get the database product name.

```java
public String getDatabaseProductName()throws SQLException
```

**5. getDatabaseProductVersion():**
 It is used to get the database product version.

```java
public String getDatabaseProductVersion()throws SQLException
```

**6. getTables(String catalog, String schemaPattern, String tableNamePattern, String[] types):**
 It is used to get the tables detail of the specified catalog.

```java
public ResultSet getTables(String catalog, String schemaPattern, String tableNamePattern, String[] types)throws SQLException
```






<br>
<br>
<br>
<br>
<br>
<br>

** **

### Examples :

** **

<br>
<br>

** **

## JDBC Statement interface


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



<br>
<br>

** **

## JDBC PreparedStatement interface


### JDBC PreparedStatement creates a table example

The JDBC PreparedStatement is used to execute parameterized queries against the database. Let us study JDBC PreparedStatement by creates a table example.

#### Example

```java
//JDBCPSCreateTest.java

package jdbc.preparedStatement;

import java.sql.Connection;
import java.sql.PreparedStatement;

import jdbc.JDBCUtil;

/**
 * This class is used to create a table in DB using PreparedStatement.
 */
public class JDBCPSCreateTest {
	public static void main(String args[]) {
		Connection conn = null;
		PreparedStatement preparedStatement = null;

		String query = "create table EMPLOYEE(" + "EMPLOYEE_ID NUMBER(5) NOT NULL, " + "NAME VARCHAR(20) NOT NULL, "
				+ "SALARY NUMBER(10) NOT NULL, " + "PRIMARY KEY (EMPLOYEE_ID) )";

		try {
			// get connection
			conn = JDBCUtil.getConnection();

			// create preparedStatement
			preparedStatement = conn.prepareStatement(query);

			// execute query
			preparedStatement.execute();

			// close connection
			preparedStatement.close();
			conn.close();

			System.out.println("Table created successfully.");
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}

```

### JDBC PreparedStatement inserts a record example

The JDBC PreparedStatement is used to execute parameterized queries against the database. Let us study JDBC PreparedStatement by inserts a record example.

#### Example

```java
package jdbc.preparedStatement;

import java.sql.Connection;
import java.sql.PreparedStatement;

import jdbc.JDBCUtil;

/**
 * This class is used to insert a record in DB table using PreparedStatement.
 */
public class JDBCPSInsertTest {
	public static void main(String args[]) {
		Connection conn = null;
		PreparedStatement preparedStatement = null;

		String query = "insert into EMPLOYEE " + "(EMPLOYEE_ID, NAME, SALARY) " + "values (?,?,?)";

		try {
			// get connection
			conn = JDBCUtil.getConnection();

			// create preparedStatement
			preparedStatement = conn.prepareStatement(query);

			// set values
			preparedStatement.setInt(1, 1);
			preparedStatement.setString(2, "John Doe");
			preparedStatement.setInt(3, 62000);

			// execute query
			preparedStatement.executeUpdate();

			// close connection
			preparedStatement.close();
			conn.close();

			System.out.println("Record inserted successfully.");
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}
```


### JDBC PreparedStatement updates a record example

The JDBC PreparedStatement is used to execute parameterized queries against the database. Let us study JDBC PreparedStatement by updates a record example.

#### Example

```java
package jdbc.preparedStatement;

import java.sql.Connection;
import java.sql.PreparedStatement;

import jdbc.JDBCUtil;

/**
 * This class is used to update a record in DB table using PreparedStatement.
 */
public class JDBCPSUpdateTest {
	public static void main(String args[]) {
		Connection conn = null;
		PreparedStatement preparedStatement = null;

		String query = "update EMPLOYEE set " + "SALARY = ? " + "where EMPLOYEE_ID = ? ";

		try {
			// get connection
			conn = JDBCUtil.getConnection();

			// create preparedStatement
			preparedStatement = conn.prepareStatement(query);

			// set values
			preparedStatement.setInt(2, 1);
			preparedStatement.setInt(1, 65000);

			// execute query
			preparedStatement.executeUpdate();

			// close connection
			preparedStatement.close();
			conn.close();

			System.out.println("Record updated successfully.");
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}

```

### JDBC PreparedStatement select records example

The JDBC PreparedStatement is used to execute parameterized queries against the database. Let us study JDBC PreparedStatement by select records example.

#### Example

```java 
package jdbc.preparedStatement;

import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;

import jdbc.JDBCUtil;

/**
 * This class is used to select a list of records from DB table using
 * PreparedStatement.
 */
public class JDBCPSSelectTest {
	public static void main(String args[]) {
		Connection conn = null;
		PreparedStatement preparedStatement = null;

		String query = "select EMPLOYEE_ID, NAME from EMPLOYEE";

		try {
			// get connection
			conn = JDBCUtil.getConnection();

			// create preparedStatement
			preparedStatement = conn.prepareStatement(query);

			// execute query
			ResultSet rs = preparedStatement.executeQuery(query);
			while (rs.next()) {
				String empId = rs.getString("EMPLOYEE_ID");
				String empName = rs.getString("NAME");

				System.out.println("EmpId : " + empId);
				System.out.println("EmpName : " + empName);
			}

			// close connection
			preparedStatement.close();
			conn.close();
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}

```

### JDBC PreparedStatement deletes a record example

The JDBC PreparedStatement is used to execute parameterized queries against the database. Let us study JDBC PreparedStatement by deletes a record example.

#### Example

```java 
package jdbc.preparedStatement;

import java.sql.Connection;
import java.sql.PreparedStatement;

import jdbc.JDBCUtil;

/**
 * This class is used to delete a record from DB table using PreparedStatement.
 */
public class JDBCPSDeleteTest {
	public static void main(String args[]) {
		Connection conn = null;
		PreparedStatement preparedStatement = null;

		String query = "delete EMPLOYEE " + "where EMPLOYEE_ID = 1 ";

		try {
			// get connection
			conn = JDBCUtil.getConnection();

			// create preparedStatement
			preparedStatement = conn.prepareStatement(query);

			// execute query
			preparedStatement.executeUpdate();

			// close connection
			preparedStatement.close();
			conn.close();

			System.out.println("Record deleted successfully.");
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}

```

### JDBC PreparedStatement batch update example

The JDBC PreparedStatement is used to execute parameterized queries against the database. Let us study JDBC PreparedStatement by batch update example.

#### Example

```java 
package jdbc.preparedStatement;

import java.sql.Connection;
import java.sql.PreparedStatement;

import jdbc.JDBCUtil;

/**
 * This class is used to batch update in DB table using PreparedStatement.
 */
public class JDBCPSBatchTest {
	public static void main(String args[]) {
		Connection conn = null;
		PreparedStatement preparedStatement = null;

		String query = "insert into EMPLOYEE " + "(EMPLOYEE_ID, NAME, SALARY) " + "values (?,?,?)";

		try {
			// get connection
			conn = JDBCUtil.getConnection();

			// set auto commit to false
			conn.setAutoCommit(false);

			// create preparedStatement
			preparedStatement = conn.prepareStatement(query);

			// set values
			preparedStatement.setInt(1, 1);
			preparedStatement.setString(2, "John Doe");
			preparedStatement.setInt(3, 62000);
			preparedStatement.addBatch();

			// set values
			preparedStatement.setInt(1, 4);
			preparedStatement.setString(2, "Jane Doe");
			preparedStatement.setInt(3, 52000);
			preparedStatement.addBatch();

			// execute query
			preparedStatement.executeBatch();

			// commit
			conn.commit();

			// close connection
			preparedStatement.close();
			conn.close();

			System.out.println("Record inserted successfully.");
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}

```

<br>
<br>

** **

## JDBC CallableStatement interface

### JDBC CallableStatement Stored procedure IN parameter example

The JDBC CallableStatement is used to execute the store procedure and functions. Let us study JDBC CallableStatement by IN parameter example.

#### Example 

```sql
//JDBC CallableStatement Stored procedure IN parameter example.

CREATE OR REPLACE PROCEDURE insertEMPLOYEE(
	   e_id IN EMPLOYEE.EMPLOYEE_ID%TYPE,
	   e_name IN EMPLOYEE.NAME%TYPE,
	   e_salary IN EMPLOYEE.SALARY%TYPE)
IS
BEGIN
 
  INSERT INTO EMPLOYEE ("EMPLOYEE_ID", "NAME", "SALARY") 
  VALUES (e_id, e_name, e_salary);
 
  COMMIT;
 
END;
```

```java
package jdbc.callableStatement;

import java.sql.CallableStatement;
import java.sql.Connection;

import jdbc.JDBCUtil;

/**
 * This class is used to insert a record in DB table using CallableStatement.
 */
public class JDBCINTest {
	public static void main(String args[]) {
		Connection conn = null;
		CallableStatement callableStatement = null;
		String proc = "{call insertEMPLOYEE(?,?,?)}";
		try {
			// get connection
			conn = JDBCUtil.getConnection();

			// create callableStatement
			callableStatement = conn.prepareCall(proc);
			callableStatement.setInt(1, 5);
			callableStatement.setString(2, "John Doe");
			callableStatement.setInt(3, 100000);

			// execute query
			callableStatement.executeUpdate();

			// close connection
			callableStatement.close();
			conn.close();

			System.out.println("Record inserted successfully.");
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}

```

### JDBC CallableStatement Stored procedure OUT parameter example

The JDBC CallableStatement is used to execute the store procedure and functions. Let us study JDBC CallableStatement by OUT parameter example.

#### Example 

```sql
//JDBC CallableStatement Stored procedure IN parameter example.
CREATE OR REPLACE PROCEDURE getEmpNameByEmpId(
	   e_id IN EMPLOYEE.EMPLOYEE_ID%TYPE,
	   e_NAME OUT EMPLOYEE.NAME%TYPE)
IS
BEGIN
 
  SELECT NAME INTO e_NAME 
  FROM  EMPLOYEE WHERE EMPLOYEE_ID = e_id;
 
END;
```

```java
package jdbc.callableStatement;

import java.sql.CallableStatement;
import java.sql.Connection;

import jdbc.JDBCUtil;

/**
 * This class is used to get a record from DB table using CallableStatement.
 */
public class JDBCOUTTest {
	public static void main(String args[]) {
		Connection conn = null;
		CallableStatement callableStatement = null;
		String proc = "{call getEmpNameByEmpId(?,?)}";
		try {
			// get connection
			conn = JDBCUtil.getConnection();

			// create callableStatement
			callableStatement = conn.prepareCall(proc);
			callableStatement.setInt(1, 5);
			callableStatement.registerOutParameter(2, java.sql.Types.VARCHAR);

			// execute query
			callableStatement.executeUpdate();

			// get employee name
			String empName = callableStatement.getString(2);
			System.out.println("Emp Name: " + empName);

			// close connection
			callableStatement.close();
			conn.close();

			System.out.println("Record inserted successfully.");
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}
```

### JDBC CallableStatement Stored procedure batch update example

The JDBC CallableStatement is used to execute the store procedure and functions. Let us study JDBC CallableStatement by batch update example.

#### Example 

```java
package jdbc.callableStatement;

import java.sql.CallableStatement;
import java.sql.Connection;

import jdbc.JDBCUtil;

/**
 * This class is used to batch update in DB table using CallableStatement.
 */
public class JDBCBatchTest {
	public static void main(String args[]) {
		Connection conn = null;
		CallableStatement callableStatement = null;
		String proc = "{call insertEMPLOYEE(?,?,?)}";
		try {
			// get connection
			conn = JDBCUtil.getConnection();

			// create callableStatement
			callableStatement = conn.prepareCall(proc);

			callableStatement.setInt(1, 7);
			callableStatement.setString(2, "John Doe");
			callableStatement.setInt(3, 50000);
			callableStatement.addBatch();

			callableStatement.setInt(1, 8);
			callableStatement.setString(2, "Jane Doe");
			callableStatement.setInt(3, 50000);
			callableStatement.addBatch();

			// execute query
			callableStatement.executeBatch();

			// close connection
			callableStatement.close();
			conn.close();

			System.out.println("Records inserted successfully.");
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}


```

** **

### JDBC store file example

PreparedStatement provides the facility to store and retrieve the file in the database using JDBC.

#### Example 

```java
package jdbc.storeRetrieveFile;

import java.io.File;
import java.io.FileReader;
import java.sql.Connection;
import java.sql.PreparedStatement;

import jdbc.JDBCUtil;

/**
 * This class is used to store a file in DB.
 */
public class JBDCstorefileTest {
	public static void main(String args[]) {
		Connection conn = null;
		PreparedStatement preparedStatement = null;

		String createTableQuery = "create table FILESTORE(" + "FILE_ID NUMBER(5) NOT NULL, " + "NAME CLOB NOT NULL, "
				+ "PRIMARY KEY (FILE_ID) )";

		try {
			// get connection
			conn = JDBCUtil.getConnection();

			// create preparedStatement
			preparedStatement = conn.prepareStatement(createTableQuery);

			// execute query for create table
			preparedStatement.execute();
			System.out.println("Table created successfully.");

			String storeFileQuery = "insert into FILESTORE " + "values (?,?)";
			preparedStatement = conn.prepareStatement(storeFileQuery);

			// Read source file
			File file = new File("F:\\test.txt");
			FileReader fileReader = new FileReader(file);

			preparedStatement.setInt(1, 2);
			preparedStatement.setCharacterStream(2, fileReader, (int) file.length());

			preparedStatement.executeUpdate();
			System.out.println("File stored successfully.");

			// close connection
			preparedStatement.close();
			conn.close();
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}

```

### JDBC retrieve file example

PreparedStatement provides the facility to store and retrieve the file in the database using JDBC.

#### Example 


```java
package jdbc.storeRetrieveFile;

import java.io.FileWriter;
import java.io.Reader;
import java.sql.Clob;
import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;

import jdbc.JDBCUtil;

/**
 * This class is used to retrieve a file from DB.
 */
public class JDBCretrieveFileTest {
	public static void main(String args[]) {
		Connection conn = null;
		PreparedStatement preparedStatement = null;

		String query = "select * from FILESTORE " + "where FILE_ID = 2";

		try {
			// get connection
			conn = JDBCUtil.getConnection();

			// create preparedStatement
			preparedStatement = conn.prepareStatement(query);

			// execute query
			ResultSet resultSet = preparedStatement.executeQuery();

			resultSet.next();

			Clob clob = resultSet.getClob(2);
			Reader reader = clob.getCharacterStream();

			FileWriter fileWriter = new FileWriter("F:\\savedFile.txt");

			int i;
			while ((i = reader.read()) != -1) {
				fileWriter.write((char) i);
			}

			System.out.println("File retrieved successfully.");

			// close connection
			fileWriter.close();
			preparedStatement.close();
			conn.close();
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}

```

** **

### JDBC retrieve file example

PreparedStatement provides the facility to store and retrieve the file in the database using JDBC.

#### Example 


















