Steps to connect JDBC
1. Import the package
2. Load and register the driver
3. Establish a connection(port number 3306,user)
4. Create statements
5. Execute the statements
6. Process the results
7. Close the connection

### 1.Import the package

import java.sql.*;

 mysql connector jar download

2.NEXT 
SELECT OPRATING SYSYEM
choose -->platform independent

3.DOWNLOAD ZIP FILE
ZIP -->UPZIP-(JAR file)

4. go to main menu-->file-->project structure-->libraries--> above click + icon-->java
5. where *mysql connector.jar*  file -->click and ok->ok-->then apply -->then ok
6. click External libraries and check where jar file will be there(where all class and interfaces will be there)
### 2.Load and register the driver(optional)

Class.forName("com.mysql.cj.jdbc.Driver)-->this will done automatically

### 3Establish a connection(port number 3306,user).

Connection is an interface 

```
String jdbcURL = "jdbc:mysql://localhost:3306/db";  
String username = "root";  
String password = "Ddstar@123";  
try (Connection connection = DriverManager.getConnection(jdbcURL, username, password)) {
```

### 4. Create statements
Statement statement = connection.createStatement();

executeQuery() for select (DQL)
executeUpdate() for DDL/DML

statement (what are can do by statement)
prepared statement (can also done by prepared statement)

Statement statement = connection.createStatement();
What it does:
connection.createStatement(): This creates a Statement object that you can use to execute SQL queries against your database.

Statement: It's an object in JDBC that allows you to send SQL queries (like SELECT, INSERT, UPDATE, DELETE) to the database and receive the results (if any).

statement: This is the variable holding the Statement object. Once you have it, you can use it to execute queries.

---
**PROBLEM 1:**


### **1. What is `Statement` in JDBC?**

- `Statement` is used to execute **static SQL queries** without parameters.
    
- It's suitable when you don’t need to reuse the SQL with different inputs.
    
- Not recommended for user inputs (unsafe, prone to SQL injection).
	
- **How it works:**  
    You write the entire SQL query as a plain string (including all values), and send it directly to the database each time you call `executeQuery()` or `executeUpdate()`.
- **No “preparing” phase:**  
    The SQL is not precompiled. Every time you run the statement, the database parses, compiles, and executes the query from scratch.

### 1. **When to Use `Statement`**

Use `Statement` **only when:**

- The SQL is **fixed/static** (no user input)
    
- You need to run **simple, one-time queries**
    
**Example:**

`Statement stmt = connection.createStatement(); stmt.executeUpdate("CREATE TABLE students (id INT, name VARCHAR(100))");`

code using statement:

```
import java.sql.*;  
public class jdbc {  
    public static void main(String[] args) {  
        String url="jdbc:mysql://localhost:3306/jd";  
        String username = "root";  
        String password = "Ddstar@123";  
  
        try(Connection connection=DriverManager.getConnection(url,username,password))  
        {  
            Statement statement=connection.createStatement();  
            System.out.println("connection created");  
  
//            String sql="create table demo(id int ,name varchar(20));";  
//            int msg=statement.executeUpdate(sql);  
//            System.out.println(msg+"succesful creayted!");  
  
//            String insert="insert into demo values(2,'ganesh')";  
//  
//            statement.executeUpdate(insert);  
//  
//            String select="desc demo";  
//  
//            ResultSet ret=statement.executeQuery(select);  
//  
//           while (ret.next())  
//           {  
//               System.out.println(ret.getInt(1)+": "+ret.getString(2));  
//           }  
            String select = "SHOW COLUMNS FROM demo";  
            ResultSet ret = statement.executeQuery(select);  
  
            while (ret.next()) {  
                System.out.println(ret.getString("Field") + ": " + ret.getString("Type"));  
            }  
  
  
        } catch (Exception e) {  
            throw new RuntimeException(e);  
        }  
  
  
    }  
}
```
---


###  **2. What is `PreparedStatement` in JDBC?**

- `PreparedStatement` is used to execute **parameterized SQL queries**.
    
- It is **precompiled** and stored in the database, so it's faster and **prevents SQL injection**.
    
- Ideal when running the **same query multiple times with different values**.
    
**You can use `PreparedStatement` to:**

- `SELECT`
    
- `INSERT`
    
- `UPDATE`
    
- `DELETE`
    
-  **Even `CREATE TABLE` or `ALTER TABLE`**
    

Though not commonly used for DDL (Data Definition Language), it **can** be used.
- You **can** use `PreparedStatement` in Java to execute **DDL commands** like `CREATE TABLE`, `ALTER TABLE`, or `DROP TABLE`.
    
- However, in **real-world usage**, `PreparedStatement` is **mostly used** for DML (Data Manipulation Language) operations — such as `SELECT`, `INSERT`, `UPDATE`, and `DELETE` — because those involve user input and benefit from **parameterization** to prevent SQL injection.
    
- DDL statements are **not dynamic or user-driven** most of the time, so developers usually use a simple `Statement` instead.
    

### Example:

```
PreparedStatement ps = conn.prepareStatement("CREATE TABLE test (id INT)");
ps.execute();

```
This works fine — the table will be created — but it's **not common practice** to do this via `PreparedStatement`.

So the line means:

> While it’s technically possible to use `PreparedStatement` for DDL, it’s not the usual or recommended practice.

### **What happens when you use PreparedStatement?**

1. **Preparation/Compilation Phase:**
    
    - When you call `conn.prepareStatement(sql)`, the SQL statement (with `?` placeholders) is sent to the database.
    - The database parses, checks, and **precompiles** (prepares an execution plan for) the SQL statement structure.
    - This is the “preparation” or “compilation” step.
    - The database remembers this plan for later executions **(as long as you use the same `PreparedStatement` object)**.
2. **Execution Phase:**
    
    - When you call `pstmt.executeUpdate()` (or `pstmt.executeQuery()`), you provide the actual data for the placeholders.
    - The database uses the **already compiled** SQL statement (from the preparation step) and just plugs in the new data.
    - **No need to recompile** the SQL each time; it just executes with new data.

---

### **3. Can you create a table using `PreparedStatement`?**

**Yes**, you can create a table using `PreparedStatement`, but it's unusual because `PreparedStatement` is mostly used with parameters and data manipulation (not DDL).

**Example:**


`String sql = "CREATE TABLE employees (id INT PRIMARY KEY, name VARCHAR(100))"; PreparedStatement pstmt = connection.prepareStatement(sql); pstmt.executeUpdate();`

Note: In this case, there are **no parameters (`?`)**, so the benefit of `PreparedStatement` is limited.

---

### **4. How to create a Connection in JDBC?**

You use `DriverManager` to create a connection, not `Statement` or `PreparedStatement`.

**Example:**

`Connection connection = DriverManager.getConnection(     "jdbc:mysql://localhost:3306/your_db", "username", "password");`

---

DESCRIBE TABLE:

- `DESC demo` won't work with `executeQuery()` in JDBC.
    
-  Use `DatabaseMetaData` for portable Java code.
    
-  Or use `SHOW COLUMNS FROM demo` for MySQL-specific code.

String select = "SHOW COLUMNS FROM demo";  
ResultSet ret = statement.executeQuery(select);  
  
while (ret.next()) {  
    System.out.println(ret.getString("Field") + ": " + ret.getString("Type"));  
}

`SHOW COLUMNS` is valid in MySQL and returns the structure of a table.

---
**code using prepared statement**

```
import java.sql.Connection;  
import java.sql.DriverManager;  
import java.sql.*;  
  
public class Preparedstateme {  
    public static void main(String[] args) {  
        String url = "jdbc:mysql://localhost:3306/jd";  
        String username = "root";  
        String password = "Ddstar@123";  
  
        try (Connection connection = DriverManager.getConnection(url, username, password)) {  
            Statement statement = connection.createStatement();  
  
//            String create="create table Prepaerd(id int  Auto_increment,name varchar(20),primary key(id))";  
//  
//            int msg=statement.executeUpdate(create);  
//            System.out.println("table creted succ "+ msg);  
  
//            String insert="insert into Prepaerd (name)values(?)";  
//  
//        PreparedStatement pre=connection.prepareStatement(insert);  
//  
//                         pre.setString(1,"manish");  
//  
//                         int inse= pre.executeUpdate();  
//            System.out.println(inse);  
  
//            String update="update  Prepaerd set name=? where id=?";  
//  
//            PreparedStatement up=connection.prepareStatement(update);  
//            up.setString(1,"john");  
//            up.setInt(2,2);  
//            up.executeUpdate();  
  
            String delete="delete from Prepaerd where id=?";  
            PreparedStatement del=connection.prepareStatement(delete);  
            del.setInt(1,1);  
            del.executeUpdate();  
            String select="select * from Prepaerd";  
            PreparedStatement sel=connection.prepareStatement(select);  
  
            ResultSet r= sel.executeQuery();  
  
            while (r.next())  
            {  
                System.out.println(r.getInt(1)+" "+r.getString(2));  
            }  
  
   String q="select * from student where id=?";  
 PreparedStatement pre=connection.prepareStatement(q);  
 pre.setInt(1,102);  
ResultSet re= pre.executeQuery();  
 while (re.next())  
 {  
     System.out.println(re.getInt(1)+" "+re.getString(2)+" "+re.getString(3));  
 }
  
  
  
        } catch (Exception e) {  
            System.out.println(e.getMessage());  
        }  
    }  
}
```

- `prepareStatement()` = set up the query (does NOT run it)
- `executeUpdate()` = actually perform the SQL action (runs it)
### Always use `PreparedStatement` for:

- Login forms
    
- Search/filter features
    
- Insert/update/delete from user input
    
- Any dynamic or repeated SQL

- **Statement:** No preparing, just sends the whole SQL query each time.
- **PreparedStatement:** The SQL structure is “prepared” (precompiled) once, and then reused with different values—this is what “preparing” means in this context.
---
**TASK 1.LIBRARY MANAGEMENT SYSTEM USING JDBC**

### 1. **Add Book**

- **Operation:** `INSERT`
- **Action:** Add a new book to the database table (e.g., `books`).
- **Example SQL:**
    
    SQL
    
    ```
    INSERT INTO books (title, author, total_copies, available_copies) VALUES (?, ?, ?, ?);
    ```
    

---

### 2. **Check Book List**

- **Operation:** `SELECT`
- **Action:** Display the list of all books (and their available copies).
- **Example SQL:**
    
    SQL
    
    ```
    SELECT * FROM books;
    ```
    

---

### 3. **Borrow Book**

- **Operation:** `UPDATE` (not `DELETE`)
- **Action:** Decrease the `available_copies` of the requested book if available (`available_copies > 0`).
- **Example SQL:**
    
    SQL
    
    ```
    UPDATE books SET available_copies = available_copies - 1 WHERE book_id = ? AND available_copies > 0;
    ```
    
- **Tip:** You may want to track who borrowed the book. For that, have a `borrowed_books` table:
    
    SQL
    
    ```
    INSERT INTO borrowed_books (book_id, user_id, borrow_date, return_date) VALUES (?, ?, ?, NULL);
    ```
    
- **Check:** If `available_copies` is 0, the book is not available.

---

### 4. **Check Book Availability**

- **Operation:** `SELECT`
- **Action:** Query the `available_copies` of the book.
- **Example SQL:**
    
    SQL
    
    ```
    SELECT available_copies FROM books WHERE book_id = ?;
    ```
    
    - If `available_copies > 0`, the book is available.

---

### 5. **Return Book**

- **Operation:** `UPDATE`
- **Action:** When a user returns a book, increase the `available_copies`.
- **Example SQL:**
    
    SQL
    
    ```
    UPDATE books SET available_copies = available_copies + 1 WHERE book_id = ?;
    ```
    
- **And update the `borrowed_books` table:**
    
    SQL
    
    ```
    UPDATE borrowed_books SET return_date = ? WHERE book_id = ? AND user_id = ? AND return_date IS NULL;
    ```
    

---

## **Summary of Database Actions**

- **Add Book:** `INSERT`
- **Borrow Book:** `UPDATE` (decrement available copies), optionally `INSERT` into `borrowed_books`
- **Check Book List/Availability:** `SELECT`
- **Return Book:** `UPDATE` (increment available copies), optionally `UPDATE` in `borrowed_books`
- **Delete:** Only used if you want to **remove a book completely** from your system (not for borrowing/returning).

---

## **You Should NOT Use DELETE for Borrowing**

- Use `UPDATE` to manage the availability.
- Use `DELETE` only for removing books from your library entirely (e.g., book is lost or outdated).

