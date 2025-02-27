### ID: 22059  
### Names: Rusimbi Patrick  
--- 
 
**Differentiation Between a Program and a Process:**

| **Aspect**              | **Program**                                                                 | **Process**                                                                 |
|-------------------------|-----------------------------------------------------------------------------|------------------------------------------------------------------------------|
| **What They Are**        | A static set of instructions stored on disk (e.g., an executable file).    | A dynamic instance of a program being executed in memory.                   |
| **State**                | Passive (not actively running).                                             | Active (executing, with a current state like running, waiting, or ready).   |
| **Lifetime**             | Persists indefinitely on storage until deleted.                             | Temporary; exists only while the program is executing.                      |
| **Resource Allocation**  | No resources (CPU, memory) are allocated to a program until it becomes a process. | Requires resources (CPU, memory, I/O) allocated by the operating system (OS). |

---

### **Why They Are Needed**
- **Program**:  
  Defines the logic and steps to perform a specific task. Without programs, computers would lack instructions to execute.  
  - Example: A `.exe` file for a calculator.

- **Process**:  
  Enables the OS to manage concurrent execution of tasks, isolate running instances, and allocate resources dynamically.  
  - Example: Running multiple instances of a browser (each as a separate process).

---

### **How They Function**
1. **Program**:  
   - Stored as a file on disk.  
   - Contains code, data, and metadata (e.g., headers for the OS).  
   - Loaded into memory by the OS when executed.  

2. **Process**:  
   - Created when a program is launched.  
   - Managed by the OS via a **Process Control Block (PCB)**, which tracks:  
     - Process state (running, waiting).  
     - CPU registers, program counter.  
     - Memory allocation (code, stack, heap).  
     - Open files, I/O devices.  
   - Executes instructions sequentially, transitioning through states (e.g., ready → running → terminated).  

---

### **Key Analogy**  
- A **program** is like a recipe (static instructions).  
- A **process** is like cooking the recipe (active execution with ingredients, utensils, and steps).  

### **Example**  
- **Program**: `notepad.exe` (stored on disk).  
- **Process**: When you open Notepad, the OS creates a process with its own memory, handles, and execution context.  

This distinction allows modern OSes to multitask (run multiple processes) efficiently while ensuring isolation and resource fairness.

### **Database: Definition, Purpose, and Usage**  
**What is a Database?**  
A database is an organized collection of structured data stored electronically, designed for efficient retrieval, modification, and management. It acts as a centralized repository controlled by a **Database Management System (DBMS)**.

**Why is it Needed?**  
- **Data Organization**: Eliminates redundancy and ensures consistency.  
- **Scalability**: Handles large volumes of data and concurrent user access.  
- **Security**: Enforces access controls and data encryption.  
- **Integrity**: Maintains accuracy with constraints (e.g., foreign keys).  
- **Querying**: Supports complex data analysis via languages like SQL.  

**How is it Used?**  
- **Applications**: Backend for websites, mobile apps, and enterprise software.  
- **Operations**: CRUD (Create, Read, Update, Delete) via APIs or SQL.  
- **Analytics**: Business intelligence, reporting, and machine learning.  

---

### **Types of Databases & DBMS Examples**  
Below are common database types with examples of DBMS and their best use cases:  

| **Type**               | **Description**                                  | **DBMS Examples**                   | **Best Example**                     |  
|------------------------|--------------------------------------------------|--------------------------------------|---------------------------------------|  
| **Relational (SQL)**    | Data stored in tables with predefined schemas.   | MySQL, PostgreSQL, Oracle           | **PostgreSQL** (open-source, robust) |  
| **Document (NoSQL)**    | Stores JSON-like documents (flexible schema).    | MongoDB, Couchbase, Firebase         | **MongoDB** (scalable, developer-friendly) |  
| **Key-Value (NoSQL)**   | Simple pairs of keys and values (fast lookups).  | Redis, DynamoDB, etcd                | **Redis** (in-memory, high-speed)     |  
| **Column-family (NoSQL)**| Optimized for columnar data storage (big data).  | Cassandra, HBase, ScyllaDB          | **Cassandra** (distributed, scalable) |  
| **Graph**               | Models relationships between entities (nodes/edges). | Neo4j, Amazon Neptune, ArangoDB | **Neo4j** (native graph processing)  |  
| **Time-Series**         | Optimized for timestamped data (IoT, monitoring). | InfluxDB, TimescaleDB, Prometheus   | **InfluxDB** (high-performance)      |  
| **Hierarchical**        | Tree-like structure (legacy systems).            | IBM IMS, XML databases, GT.M        | **IBM IMS** (enterprise mainframes)  |  
| **Object-Oriented**     | Stores objects (classes/attributes).             | db4o, ObjectDB, Versant             | **ObjectDB** (Java/.NET integration) |  

---

### **Key Use Cases**  
1. **Relational**: Financial systems, ERP (e.g., PostgreSQL for ACID compliance).  
2. **Document**: Content management, e-commerce (e.g., MongoDB for flexible schemas).  
3. **Key-Value**: Caching, session management (e.g., Redis for real-time apps).  
4. **Graph**: Social networks, fraud detection (e.g., Neo4j for relationship analysis).  
5. **Time-Series**: IoT sensor data, stock trading (e.g., InfluxDB for high-speed ingestion).  

Databases and their DBMS are foundational to modern computing, enabling structured data storage, retrieval, and analysis across industries.
### **`st.execute(sql)` Return Values in JDBC**  
In Java JDBC, `st.execute(sql)` (where `st` is a `Statement` object) returns a **boolean** indicating whether the executed SQL statement produced a result set. Here’s a breakdown:

---

### **1. When `st.execute(sql)` Returns `true`**  
**Condition**: The SQL statement is a **query** that returns a result set (e.g., `SELECT`).  

**Example**:  
```java
String sql = "SELECT * FROM employees WHERE department = 'Sales'";
boolean hasResult = st.execute(sql); // Returns true

if (hasResult) {
    ResultSet rs = st.getResultSet(); // Retrieve the result set
    while (rs.next()) {
        System.out.println(rs.getString("name"));
    }
}
```

---

### **2. When `st.execute(sql)` Returns `false`**  
**Condition**: The SQL statement is a **non-query** (e.g., `INSERT`, `UPDATE`, `DELETE`, DDL like `CREATE`, or DML without a result set).  

**Example**:  
```java
String sql = "INSERT INTO employees (name, department) VALUES ('Alice', 'Engineering')";
boolean hasResult = st.execute(sql); // Returns false

if (!hasResult) {
    int rowsAffected = st.getUpdateCount(); // Get number of rows modified
    System.out.println(rowsAffected + " row(s) inserted.");
}
```

---

### **Key Notes**  
- **DDL Statements** (e.g., `CREATE TABLE`, `ALTER`) also return `false` because they do not produce result sets.  
  ```java
  String sql = "CREATE TABLE departments (id INT PRIMARY KEY, name VARCHAR(50))";
  boolean hasResult = st.execute(sql); // Returns false
  ```
- Use `st.getResultSet()` **only** if `execute()` returns `true`.  
- Use `st.getUpdateCount()` to check affected rows for `INSERT`, `UPDATE`, `DELETE`, etc.  

---

### **Summary Table**  
| **SQL Type**          | **Example Query**                          | **Return Value** | **Method to Use After**       |  
|------------------------|--------------------------------------------|------------------|-------------------------------|  
| Query (`SELECT`)       | `SELECT * FROM employees`                 | `true`           | `st.getResultSet()`           |  
| Non-Query (`INSERT`/`UPDATE`) | `DELETE FROM employees WHERE id = 101` | `false`          | `st.getUpdateCount()`         |  
| DDL (`CREATE TABLE`)   | `CREATE TABLE projects (...)`             | `false`          | `st.getUpdateCount()` (often `0`) |  

This distinction ensures proper handling of result sets and data modification operations in JDBC.
### **Why Closing a JDBC Connection is Essential**  
Closing a JDBC connection is critical for resource management, performance, and reliability in database-driven applications. Here’s why:

---

#### **1. Resource Management**  
- **Database Server Limits**: Databases allow a finite number of concurrent connections. Unclosed connections exhaust this limit, blocking new requests.  
- **Memory Leaks**: JDBC connections consume memory (on both the application and database sides). Failing to close them leads to memory bloat and eventual crashes.  
- **Connection Pool Efficiency**: Most apps use connection pools (e.g., HikariCP). Unclosed connections are not returned to the pool, starving the application of available connections.  

---

#### **2. Transaction and Lock Management**  
- **Uncommitted Transactions**: Open connections may leave transactions incomplete, causing data inconsistency.  
- **Database Locks**: Connections can hold locks on tables/rows, blocking other processes and leading to deadlocks.  

---

#### **3. Preventing Resource Starvation**  
- **Example**: A loop creating connections without closing them:  
  ```java  
  while (true) {  
      Connection conn = DriverManager.getConnection(url);  
      // Do something but forget to close...  
  }  
  ```  
  This rapidly crashes the app/database due to resource exhaustion.  

---

#### **4. Best Practices**  
- **Use `try-with-resources` (Java 7+)** to auto-close connections:  
  ```java  
  try (Connection conn = DriverManager.getConnection(url);  
       Statement st = conn.createStatement()) {  
      // Execute queries  
  } // conn.close() is called automatically  
  ```  
- **Explicitly Close in Legacy Code**:  
  ```java  
  Connection conn = null;  
  try {  
      conn = DriverManager.getConnection(url);  
      // Work with connection  
  } finally {  
      if (conn != null) conn.close(); // Ensure cleanup  
  }  
  ```  

---

### **What Happens If You Don’t Close?**  
- **Short-Term**: Minor performance degradation.  
- **Long-Term**:  
  - Database rejects new connections (e.g., `Too many connections` error in MySQL).  
  - Application crashes due to `OutOfMemoryError`.  
  - Degraded user experience (slow responses, timeouts).  

---

### **In a nutshell**  
Closing JDBC connections ensures:  
- Efficient resource reuse (via pools).  
- Stability for both the app and database.  
- Prevention of memory leaks and deadlocks.  

**Always close connections in a `finally` block or use `try-with-resources`!**
