# JDBC
The JDBC (Java Database Connectivitiy) is an API that is used to create a connection between a Java application and anyone one of many standard database applications. JDBC provides the functionality to execute SQL statements on our database as well.

## Components / Architecture
There are five primary layers in architecture of the program:

### Application
This is the standard Java application that you are used to working with. It includes all the logic, user interface, and implementation of the core OOP principles.

### JDBC API
This is a set of classes and supporting files that provide the framework for the connection to a database. The API comes standard as a part of the JDK, so you won’t need to download any additional packages, but you will need to import the parts of the API that you will be using into your program.

### JDBC Driver Manager
The JDBC driver manager, normally referenced by importing and calling the `DriverManager` class acts as the interface between you the programmer, and the actual drivers for the database. Inside the class are all the methods needed to register and deregister the specific drivers, and open and close the connection between your program and the database. One important aspect is that this class maintains a registry of all the drivers that have registered with the program. Driver registration is a mandatory part of the database connection process.

### JDBC Drivers
This is the specific code that translates the commands sent via the JDBC into the language and syntax that the designated database works with. Most database applications, MySQL, SQLite, and Postgres for example, each provide JDBC drivers that can be downloaded from their websites. It is not uncommon for these drivers to be a blend of the Java language and some other language that is used in the database. These drivers need to be imported directly into the classpath of the program (adding the `.jar` to your program through your IDE. In older versions of Java, it was necessary to explicitly register a driver but since JDBC 4.0 the `DriverManager` is capable of detecting and loading drivers that are present at compile time.

### Databases
These are the data storage objects used to persist data throughout your application. There are many different vendors providing data storage solutions and each has its own set of advantages and disadvantages. As a developer, it may be your job to compare databases and decide which one works best for your application.

## Establishing a JDBC Connection

### Importing Drivers and JDBC Classes
First, you need to download the proper driver for the database you are using. You will need to include the `.jar` file in with your project. Once the driver is included in the classpath, you can start importing classes from `java.sql`:
```java
import java.sql.DriverManager; // Provides the methods to establish the DB connection
import java.sql.SQLException;  // Provides error handling when interacting with the DB
import java.sql.Connection;    // Manages the connection and statements
import java.sql.Statement;     // Executes queries on the DB
import java.sql.ResultSet;     // The results of a query
```

### Connecting to the Database
To open the connection, call the `DriverManager::getConnection(url, username, password)` method which returns a `Connection` object.

*Note: These connections and operators are very costly in both network resources and program memory. The best practice is to use a `try-with-resources` block. This eiliminates the need to add a `finally` block to our `try-catch` statements.*

```java
import java.sql.*;

public class TryBlockExamples {
  public static void main(String[] args) {
    String url = "host:db:port";
    String userName = "admin";
    String password = "adminPassword";
    
    /*
    Try - Catch - Finally syntax. The resources are declared outside of the try block
    and then closed in the finally block. If this finally block is forgotten, the resources
    are left open.
     */
    
    Connection conn = null;
    Statement statement = null;
    ResultSet results = null;

    try {
      conn = DriverManager.getConnection(url, userName, password);
      statement = conn.createStatement();
      results = statement.executeQuery("SELECT * FROM SOMETABLE");
      // Do something with results
    } catch (SQLException e) {
      System.out.println(e.getMessage());
    } finally {
      try { results.close(); } catch (Exception e) { /* Ignored */ }
      try { statement.close(); } catch (Exception e) { /* Ignored */ }
      try { conn.close(); } catch (Exception e) { /* Ignored */ }
    }
    
    /*
    Try With Resources block, the resources are now a part of the try block itself
    and the closing of the resources is handled automatically at the end of the execution.
     */
    
    try (Connection conn1 = DriverManager.getConnection(url, userName, password); 
         Statement statement1 = conn.createStatement(); 
         ResultSet results1 = statement.executeQuery("SELECT * FROM SOMETABLE");
    ) {
      // Do something with results
    } catch (SQLException e) {
      System.out.println(e.getMessage());
    }
  }
}
```

### Statements and Executing Queries

To execute SQL statements, create a new instance of a `Statement` object from a `Connection` object. For more complex SQL operations such as passing in parameters or other logic dependent code use a `PreparedStatement`.

```java
Statment s = connection.createStatement();
```

### Interacting with the Results
After statements are executed, a `ResultSet` object is returned. A `ResultSet` can be thought of as a 2D array that corresponds to the table from the database.
```java
// Retrieve results
ResultSet results = s.executeQuery("SELECT * FROM sometable");

// Update the database
s.executeUpdate("CREATE TABLE CUSTOMERS");
```
The `ResultSet` is a cursor to the first row. Use the `.next()` method to move the cursor to the next row. To access information in a row, use a `getX` method, where `X` is the matching datatype of the column with an index for the column (1-based). 

