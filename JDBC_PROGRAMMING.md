# JDBC PROGRAMMING

## 1. What is JDBC? List out all various types of JDBC Driver.Explain Thick and Thin driver

### JDBC

- JDBC stands for Java Database Connectivity.
- JDBC is a Java API to connect and execute the query with the database.
- It is a part of JavaSE (Java Standard Edition).
- JDBC API uses JDBC drivers to connect with the database.

### Type of JDBC driver

1. Type 1 − JDBC-ODBC Bridge Driver
2. Type 2 − Native Code Driver/JNI
3. Type 3 − Java Protocol/Middleware
4. Type 4 − Database Protocol

### Thick and Thin driver

- If Driver won’t require any extra Component to communicate with Database, such type of Driver is called Thin Driver.

- E.g: Type-4 Driver

- If Driver require some extra Component (like ODBC Driver OR Vendor specific Native Libraries OR Middleware Server), such Type of Driver is called Thick Driver.

- E.g: Type-1, Type-2 and Type-3 Drivers

## 2. Explain JDBC driver types in detail

- JDBC drivers are client-side adapters (installed on the client machine, not on the server) that convert requests from Java programs to a protocol that the DBMS can understand.
- There are 4 types of JDBC drivers:

1. Type 1 − JDBC-ODBC Bridge Driver
2. Type 2 − Native Code Driver/JNI
3. Type 3 − Java Protocol/Middleware
4. Type 4 − Database Protocol

### Type 1 − JDBC-ODBC Bridge Driver

- Depends on support for ODBC
- Not portable
- ODBC must be set up on every client
- No support from JDK 1.8(Java 8)
- Translate JDBC calls into ODBC calls and use Windows ODBC built in drivers
- E.g MS Access

#### Advantages: Type 1

- Allow to communicate with all database supported by ODBC driver
- it is vendor independent driver

#### Disadvatages: Type 1

- Due to large number of translations, execution speed is decreased
- Dependent on the ODBC driver
- ODBC binary code or ODBC client library to be installed in every client machine
- Uses java native interface to make ODBC call

- Because of listed disadvantage, type 1 driver is not used in production environment.
- It can only be used, when database doesn’t have any other JDBC driver implementation.

![JDBC-ODBC Bridge Driver](https://www.tutorialspoint.com/jdbc/images/dbms_driver_type1.jpg)

### Type 2 − Native Code Driver/JNI

- JDBC API calls are converted into native API calls, which are unique to
  the database.
- These drivers are typically provided by the database vendors and used
  in the same manner as the JDBC-ODBC Bridge.
- Native code Driver are usually written in C, C++.
- The vendor-specific driver must be installed on each client machine.
- Type 2 Driver is suitable to use with server side applications.
- E.g. Oracle OCI driver, Weblogic OCI driver, Type2 for Sybase

#### Advantages: Type 2

- As there is no implementation of JDBC-ODBC bridge, it may be considerably faster
  than a Type 1 driver.

#### Disadvantages: Type 2

- The vendor client library needs to be installed on the client machine.
- This driver is platform dependent.
- This driver supports all java applications except applets.
- It may increase cost of application, if it needs to run on different platform (since we
  may require buying the native libraries for all of the platform).

![Native Code Driver/JNI](https://www.tutorialspoint.com/jdbc/images/dbms_driver_type2.jpg)

### Type 3 − Java Protocol/Middleware

- Pure Java Driver
- Depends on Middleware server
- Can interface to multiple databases – Not vendor specific.
- Follows a three-tier communication approach.
- The JDBC clients use standard network sockets to communicate with a middleware
  application server.
- The socket information is then translated by the middleware application server into
  the call format required by the DBMS.
- This kind of driver is extremely flexible, since it requires no code installed on the
  client and a single driver can actually provide access to multiple databases.

#### Advantages: Type 3

- Since the communication between client and the middleware server is database
  independent, there is no need for the database vendor library on the client.
- A single driver can handle any database, provided the middleware supports it.
- We can switch from one database to other without changing the client-side driver
  class, by just changing configurations of middleware server.
- E.g.: IDS Driver, Weblogic RMI Driver

#### Disadvantages: Type 3

- Compared to Type 2 drivers, Type 3 drivers are slow due to increased number of
  network calls.
- Requires database-specific coding to be done in the middle tier.
- The middleware layer added may result in additional latency, but is typically
  overcome by using better middleware services.

![Java Protocol/Middleware](https://www.tutorialspoint.com/jdbc/images/dbms_driver_type3.jpg)

### Type 4 − Database Protocol

- It is known as the Direct to Database Pure Java Driver
- Need to download a new driver for each database engine
  e.g. Oracle, MySQL
- Type 4 driver, a pure Java-based driver communicates directly with the vendor's
  database through socket connection.
- This kind of driver is extremely flexible, you don't need to install special software on
  the client or server.
- Such drivers are implemented by DBMS vendors.

#### Advantages: Type 4

- Completely implemented in Java to achieve platform independence.
- No native libraries are required to be installed in client machine.
- These drivers don't translate the requests into an intermediary format (such as
  ODBC).
- Secure to use since, it uses database server specific protocol.
- The client application connects directly to the database server.
- No translation or middleware layers are used, improving performance.

#### Disadvantages: Type 4

- This Driver uses database specific protocol and it is DBMS vendor dependent.

![Database Protocol](https://www.tutorialspoint.com/jdbc/images/dbms_driver_type4.jpg)

## 3. Comparison between JDBC Drivers

![Comparison between JDBC Drivers](https://miro.medium.com/max/640/0*5N1nZNpfm3OZ6t0t.jpg)

## 4. JDBC program

`JDBCProcess.java`

```java
import java.sql.*;

public class JDBCProcess{
    public static void main(String[] args) throws Exception{

        Class.forName("com.mysql.cj.jdbc.Driver");

        String url = "jdbc:mysql://localhost:3306/photo_store";
        String username = "root";
        String password = "jaydeep";

        Connection conn = DriverManager.getConnection(url, username, password);
        
        Statement stmt = conn.createStatement();

        ResultSet rs = stmt.executeQuery("SELECT * FROM canon_cameras");

        while (rs.next()) {
            System.out.print(rs.getString("model_name") + "\t");
            System.out.println(rs.getInt("quantity") + "\t");
        }

        rs.close();
        stmt.close();
        conn.close();

    }
}
```

`OUTPUT`

```cmd
70-D    12
80D     19
EOS-R   25
EOS-r5  80
EOR-r6  50
```

## 5. PreparedStatement that insert the record

`PreparedInsert.java`

```java
import java.sql.*;

public class PreparedInsert{
    public static void main(String[] args) throws Exception{
        
        Class.forName("com.mysql.cj.jdbc.Driver");

        String url = "jdbc:mysql://localhost:3306/photo_store";
        String username = "root";
        String password = "jaydeep";

        Connection conn = DriverManager.getConnection(url, username, password);
        
        String query = "insert into students values(?,?,?,?)";

        PreparedStatement ps = conn.prepareStatement(query);

        ps.setString(1, "786");
        ps.setString(2, "xyz");
        ps.setString(3, "it");
        ps.setString(4, "cz");

        int noRows = ps.executeUpdate();

        System.out.println("number of rows updated = " + noRows);

        ps.close();
        conn.close();
    }
}
```

`OUTPUT:`

```cmd
number of rows updated = 1
```

## 6. CallableStatement

```mysql
create table book (
 isbn INT,
 title VARCHAR(50),
 author VARCHAR(50)
);
insert into book (isbn, title, author) values (95, 'Four Minutes (Vier Minuten)', 'Faun Harbottle');
insert into book (isbn, title, author) values (31, 'Act in Question, The (Acto en cuestión, El)', 'Stevy Eadington');
insert into book (isbn, title, author) values (4, '7 Dollars on the Red (Sette dollari sul rosso)', 'Melisande Schurcke');
insert into book (isbn, title, author) values (58, 'Diary of a Lost Girl (Tagebuch einer Verlorenen)', 'Eustacia Vivian');
insert into book (isbn, title, author) values (53, 'Sicko', 'Marijn Bumpas');
```

```cmd
+------+---------------------------------------------+------------------+
| isbn | title                                       | author           |
+------+---------------------------------------------+------------------+
|   38 | Guest House Paradiso                        | Jilli Sinclar    |
|   21 | 100 Bloody Acres                            | Faulkner Salmoni |
|   18 | Jew in the Lotus, The                       | Rianon Scoular   |
|   98 | Wind and the Lion, The                      | Vale Serotsky    |
|   77 | Too Beautiful for You (Trop belle pour toi) | Tawnya Linfoot   |
+------+---------------------------------------------+------------------+
```

```mysql
DELIMITER //
CREATE PROCEDURE gettitle
(IN isbn_no INT, OUT btitle VARCHAR(50))
BEGIN
  SELECT title INTO btitle
  FROM  book
  WHERE isbn_no = isbn;
END //
DELIMITER ;
```

`CallableDemo.java`

```java
import java.sql.*;

public class CallableDemo{
    public static void main(String[] args) throws Exception {
        Class.forName("com.mysql.cj.jdbc.Driver");

        String url = "jdbc:mysql://localhost:3306/photo_store";
        String username = "root";
        String password = "jaydeep";

        Connection conn = DriverManager.getConnection(url, username, password);

        CallableStatement cs = conn.prepareCall("{call gettitle(?,?)}");

        cs.setInt(1,21);
        cs.registerOutParameter(2, Types.VARCHAR);
        cs.execute();

        System.out.println(cs.getString(2));
        
        cs.close();
        conn.close();

    }
}
```

`OUTPUT`

```cmd
100 Bloody Acres
```

## 7. Update record using ResultSet interface

`UpdateDemo.java`

```java
import java.sql.*;

public class UpdateDemo{
    public static void main(String[] args) throws Exception{

        Class.forName("com.mysql.cj.jdbc.Driver");

        String url = "jdbc:mysql://localhost:3306/photo_store";
        String username = "root";
        String password = "jaydeep";

        Connection conn = DriverManager.getConnection(url, username, password);
        
        Statement stmt = conn.createStatement(ResultSet.TYPE_SCROLL_SENSITIVE, ResultSet.CONCUR_UPDATABLE);

        ResultSet rs = stmt.executeQuery("SELECT * FROM book");

        System.out.println("Contents of the book table before the update: ");
        while(rs.next()) {
            System.out.print("ID: "+rs.getInt("isbn")+", ");
            System.out.print("TITLE: "+rs.getString("title")+", ");
            System.out.print("AUTHOR: "+rs.getString("author")+", ");
            System.out.println();
        }

        rs.beforeFirst();

        while(rs.next()) {
            if(rs.getInt("isbn")==98) {
                rs.updateString("title","xxx");
                rs.updateString("author","sins");
                rs.updateRow();
            }
        }

        rs.beforeFirst();

        System.out.println("Contents of the book table after the update: ");
        while(rs.next()) {
            System.out.print("ID: "+rs.getInt("isbn")+", ");
            System.out.print("TITLE: "+rs.getString("title")+", ");
            System.out.print("AUTHOR: "+rs.getString("author")+", ");
            System.out.println();
        }
    }
}

```

`OUTPUT`

```java
Contents of the book table before the update:
ID: 18, TITLE: Jew in the Lotus, The, AUTHOR: Rianon Scoular,
ID: 21, TITLE: 100 Bloody Acres, AUTHOR: Faulkner Salmoni,
ID: 38, TITLE: Guest House Paradiso, AUTHOR: Jilli Sinclar,
ID: 77, TITLE: Too Beautiful for You (Trop belle pour toi), AUTHOR: Tawnya Linfoot,
ID: 98, TITLE: xxx, AUTHOR: Vale Serotsky,
Contents of the book table after the update:
ID: 18, TITLE: Jew in the Lotus, The, AUTHOR: Rianon Scoular,
ID: 21, TITLE: 100 Bloody Acres, AUTHOR: Faulkner Salmoni,
ID: 38, TITLE: Guest House Paradiso, AUTHOR: Jilli Sinclar,
ID: 77, TITLE: Too Beautiful for You (Trop belle pour toi), AUTHOR: Tawnya Linfoot,
ID: 98, TITLE: xxx, AUTHOR: sins,
```

## 8. ResultSetMetaDeta

`ResultSetMetaDetaDemo.java`

```java
import java.sql.*;

public class ResultSetMetaDataDemo{
    public static void main(String[] args) throws Exception{

        Class.forName("com.mysql.cj.jdbc.Driver");

        String url = "jdbc:mysql://localhost:3306/photo_store";
        String username = "root";
        String password = "jaydeep";

        Connection conn = DriverManager.getConnection(url, username, password);
        
        Statement stmt = conn.createStatement();

        ResultSet rs = stmt.executeQuery("SELECT * FROM book");

        ResultSetMetaData rsmd = rs.getMetaData();

        System.out.println("Total columns : " + rsmd.getColumnCount());
        System.out.println("Column name of 1st column : " + rsmd.getColumnName(1));
        System.out.println("Column type name of 1st column : " + rsmd.getColumnTypeName(1));

        rs.close();
        stmt.close();
        conn.close();

    }
}
```

`OUTPUT`

```cmd
Total columns : 3
Column name of 1st column : isbn
Column type name of 1st column : INT
```

## 9. DatabaseMetaData

`DatabaseMetaDataDemo.java`

```java
import java.sql.*;

public class DatabaseMetaDataDemo{
    public static void main(String[] args) throws Exception{

        Class.forName("com.mysql.cj.jdbc.Driver");

        String url = "jdbc:mysql://localhost:3306/photo_store";
        String username = "root";
        String password = "jaydeep";

        Connection conn = DriverManager.getConnection(url, username, password);
        
        DatabaseMetaData dbmd = conn.getMetaData();

        System.out.println("Driver Name: "+dbmd.getDriverName());  
        System.out.println("Driver Version: "+dbmd.getDriverVersion());  
        System.out.println("UserName: "+dbmd.getUserName());  
        System.out.println("Database Product Name: "+dbmd.getDatabaseProductName());  
        System.out.println("Database Product Version: "+dbmd.getDatabaseProductVersion());  
        System.out.println("getURL(): "+dbmd.getURL());
    }
}

```

`OUTPUT`

```cmd
Driver Name: MySQL Connector/J
Driver Version: mysql-connector-java-8.0.29 (Revision: dd61577595edad45c398af508cf91ad26fc4144f)
UserName: root@localhost
Database Product Name: MySQL
Database Product Version: 8.0.29
getURL(): jdbc:mysql://localhost:3306/photo_store
```

## 10. SQL UPDATE

`SQLUpdateDemo.java`

```java
import java.sql.*;

public class SQLUpdateDemo{
    public static void main(String[] args) throws Exception{

        Class.forName("com.mysql.cj.jdbc.Driver");

        String url = "jdbc:mysql://localhost:3306/photo_store";
        String username = "root";
        String password = "jaydeep";

        Connection conn = DriverManager.getConnection(url, username, password);
        
        Statement stmt = conn.createStatement();

        String query = "update book set author = 'johnny' where isbn = 98";

        int noRows = stmt.executeUpdate(query);

        System.out.println("total number of rows updated : " + noRows);

        stmt.close();
        conn.close();

    }
}
```

`OUTPUT`

```cmd
total number of rows updated : 1
```

## 11. Transaction Management : commit & rollback

`CommitRollbackDemo.java`

```java
import java.sql.*;

public class CommitRollbackDemo{
    public static void main(String[] args) throws Exception{

        Class.forName("com.mysql.cj.jdbc.Driver");

        String url = "jdbc:mysql://localhost:3306/photo_store";
        String username = "root";
        String password = "jaydeep";

        Connection conn = DriverManager.getConnection(url, username, password);

        conn.setAutoCommit(false);

        Statement stmt = conn.createStatement();
        
        int noRows = stmt.executeUpdate("insert into students values(2,'urvi','xaf','cy')");

        conn.commit();

        noRows += stmt.executeUpdate("insert into students values(3,'riddhi','xa','cy')");

        System.out.println("number of rows inserted = " + noRows);
        
        conn.rollback();

        conn.close();
    }
}
```

`OUTPUT`

```cmd
number of rows inserted = 2
```

`TABLE BEFORE`

```cmd
+-----+------+--------+----------+
| no  | name | branch | division |
+-----+------+--------+----------+
| 786 | xyz  | it     | cz       |
+-----+------+--------+----------+
```

`TABLE AFTER`

```cmd
+-----+------+--------+----------+
| no  | name | branch | division |
+-----+------+--------+----------+
| 2   | urvi | xaf    | cy       |
| 786 | xyz  | it     | cz       |
+-----+------+--------+----------+
```

## 12. Batch Processing in JDBC

`BatchProcessingDemo.java`

```java
import java.sql.*;

public class BatchProcessingDemo{
    public static void main(String[] args) throws Exception{

        Class.forName("com.mysql.cj.jdbc.Driver");

        String url = "jdbc:mysql://localhost:3306/photo_store";
        String username = "root";
        String password = "jaydeep";

        Connection conn = DriverManager.getConnection(url, username, password);
        
        Statement stmt = conn.createStatement();

        String query1, query2, query3, query4, query5, query6, query7;

        query1 = "create table DietStudent(enr INT PRIMARY KEY, name VARCHAR(20), sem INT, branch VARCHAR(10))";

        query2 = "insert into DietStudent values(6001,'urvi',6,'ce')";
        query3 = "insert into DietStudent values(6002,'priyanshi',6,'ce')";
        query4 = "insert into DietStudent values(6003,'aj',6,'ce')";
        query5 = "insert into DietStudent values(6004,'cj',6,'ce')";

        query6 = "update DietStudent set name='jd' where enr=6003";

        query7 = "delete from DietStudent where name = 'cj'";

        stmt.addBatch(query1);
        stmt.addBatch(query2);
        stmt.addBatch(query3);
        stmt.addBatch(query4);
        stmt.addBatch(query5);
        stmt.addBatch(query6);
        stmt.addBatch(query7);

        // int[] i = stmt.executeBatch();
        stmt.executeBatch();

        conn.close();
    }
}
```

`SELECT * FROM dietstudent;`

```cmd
+------+-----------+------+--------+
| enr  | name      | sem  | branch |
+------+-----------+------+--------+
| 6001 | urvi      |    6 | ce     |
| 6002 | priyanshi |    6 | ce     |
| 6003 | jd        |    6 | ce     |
+------+-----------+------+--------+
```

## 13. Transaction Isolation Level : Program

`IsolationDemo.java`

```java
import java.sql.*;

public class IsolationDemo{
    public static void main(String[] args) throws Exception{

        Class.forName("com.mysql.cj.jdbc.Driver");

        String url = "jdbc:mysql://localhost:3306/photo_store";
        String username = "root";
        String password = "jaydeep";

        Connection conn = DriverManager.getConnection(url, username, password);
        
        Statement stmt = conn.createStatement();

        System.out.println(conn.getTransactionIsolation());

        conn.setTransactionIsolation(Connection.TRANSACTION_SERIALIZABLE);

        System.out.println(conn.getTransactionIsolation());

        stmt.close();
        conn.close();
    }
}
```

`OUTPUT`

```cmd
4
8
```

## 14. Code to store image in database

`MYSQL: CREATE TABLE | cats`

```sql
CREATE TABLE cats (
    `id` INTEGER UNSIGNED NOT NULL AUTO_INCREMENT
        PRIMARY KEY,
    `img` LONGBLOB NOT NULL
)
```

`StoreImage.java`

```java
import java.sql.*;
import java.io.FileInputStream;
import java.io.InputStream;

public class StoreImage{
    public static void main(String[] args) throws Exception{

        Class.forName("com.mysql.cj.jdbc.Driver");

        String url = "jdbc:mysql://localhost:3306/photo_store";
        String username = "root";
        String password = "jaydeep";

        Connection conn = DriverManager.getConnection(url, username, password);
        
        PreparedStatement ps = conn.prepareStatement("INSERT INTO cats VALUES(?,?)");

        ps.setInt(1, 430);
       
        InputStream in = new FileInputStream("chad.jpg");

        ps.setBlob(2, in);
  
        ps.execute();

        conn.close();
    }
}
```

`chad.jpg`

![fun](https://scontent.fraj2-1.fna.fbcdn.net/v/t1.6435-9/84955915_2702372329845689_7952059831748132864_n.jpg?_nc_cat=109&ccb=1-7&_nc_sid=8bfeb9&_nc_ohc=EbbBIV7JoC4AX_t_hN4&_nc_oc=AQncaVHfQwk_EOVaDNqVBv-S3SYuM6Nls5sTbjYqu5sz4uW_mxRgvGToxZ-9rgvtQE0&_nc_ht=scontent.fraj2-1.fna&oh=00_AfAhZfetGYqj83xfrU_X0gQCk1c2L2_PQtNCI0i3aO7K1w&oe=6429C293)
