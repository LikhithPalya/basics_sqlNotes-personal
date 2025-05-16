## find the live link here - https://likhithpalya.github.io/basics_sqlNotes-personal/

### Basic SQL Queries:

*   **How do you retrieve all records from a table?**

    To retrieve all records from a table, you can use the `SELECT` statement with an asterisk (`*`) wildcard character, followed by the `FROM` keyword and the table name. For example:

    ```sql
    SELECT *
    FROM Customers;
    ```
*   **How can you fetch only distinct values in SQL?**

    To retrieve only distinct (unique) values from a table, you can use the `DISTINCT` keyword in the `SELECT` statement. For example:

    ```sql
    SELECT DISTINCT Country
    FROM Customers;
    ```
*   **What is the difference between WHERE and HAVING clauses?**

    The `WHERE` clause is used to filter rows **before** grouping, while the `HAVING` clause is used to filter groups **after** grouping. For example:
    ```sql
    -- Filter customers who are from 'Mexico' then group
    SELECT COUNT(*), Country
    FROM Customers
    WHERE Country = 'Mexico'
    GROUP BY Country;

    -- Group all customers, then filter out groups with less than two customers.
    SELECT COUNT(*), Country
    FROM Customers
    GROUP BY Country
    HAVING COUNT(*) > 2;
    ```
*   **How do you sort the results of a query in ascending or descending order?**

    You can sort the results of a query in ascending or descending order using the `ORDER BY` clause followed by the column name and the sort order (`ASC` for ascending, `DESC` for descending). For example:

    ```sql
    SELECT *
    FROM Customers
    ORDER BY Country ASC, CustomerName DESC;
    ```
*   **Explain the LIMIT clause and its use.**

    The `LIMIT` clause is used to limit the number of rows returned by a query. For example:

    ```sql
    SELECT *
    FROM Customers
    LIMIT 10;
    ```
*   **How can you count the number of records in a table?**

    You can count the number of records in a table by using the `COUNT(*)` function. For example:

    ```sql
    SELECT COUNT(*)
    FROM Customers;
    ```
*   **What is the purpose of the GROUP BY clause?**

    The `GROUP BY` clause is used to group rows with the same values in one or more columns into a summary row. For example:

    ```sql
    SELECT COUNT(*), Country
    FROM Customers
    GROUP BY Country;
    ```
*   **How do you filter data using multiple conditions?**

    You can filter data using multiple conditions by combining them using the `AND` and `OR` operators. For example:

    ```sql
    SELECT *
    FROM Customers
    WHERE Country='Mexico' AND City='Mexico City';
    ```
*   **What is the IN operator and how is it used?**

    The `IN` operator is used to check if a value matches any value in a list or a subquery. For example:

    ```sql
    SELECT *
    FROM Customers
    WHERE Country IN ('Mexico', 'Canada', 'USA');
    ```
*   **How do you update a specific record in a table?**

    You can update a specific record in a table by using the `UPDATE` statement along with the `WHERE` clause to specify the record to be updated. For example:

    ```sql
    UPDATE Customers
    SET ContactName = 'Alfred Schmidt', City= 'Frankfurt'
    WHERE CustomerID = 1;
    ```

### Joins

*   **What are the different types of joins in SQL?**

    The different types of joins in SQL are:

    *   **INNER JOIN:** Returns rows only when there is a match in both tables.
    *   **LEFT JOIN:** Returns all rows from the left table, even if there is no match in the right table.
    *   **RIGHT JOIN:** Returns all rows from the right table, even if there is no match in the left table.
    *   **FULL JOIN:** Returns all rows from both tables, regardless of whether there is a match.
    *   **CROSS JOIN:** Returns the Cartesian product of the two tables, which means that every row in the first table is joined with every row in the second table.
    *   **SELF JOIN:** This is when a table is joined to itself.
*   **Explain the difference between INNER JOIN and OUTER JOIN.**

    An **INNER JOIN** returns rows only when there is a match in both tables based on the join condition. An **OUTER JOIN**, on the other hand, returns rows from one or both tables, even if there is no match.
*   **How does a LEFT JOIN work?**

    A **LEFT JOIN** returns all rows from the left table (the table mentioned before `LEFT JOIN`) and the matching rows from the right table (the table mentioned after `LEFT JOIN`). If there is no match, the result set will contain `NULL` values for the columns of the right table.
*   **What is a CROSS JOIN and when would you use it?**

    A **CROSS JOIN**, also known as a Cartesian Join, combines each row from the first table with every row from the second table, resulting in a result set that is the product of the number of rows in each table. 

    You would use a `CROSS JOIN` in situations where you need to generate all possible combinations of rows between two tables. For instance: you have a table of shirt colors and a table of pant sizes. A `CROSS JOIN` would allow you to generate all possible outfit combinations. 
*   **Can you explain the use of a SELF JOIN?**

    A **SELF JOIN** is used to join a table to itself, effectively treating it as two separate tables. This is useful for querying hierarchical data or comparing rows within the same table. For example, finding all employees who report to another employee in the same table.
*   **What is the difference between UNION and UNION ALL?**

    Both `UNION` and `UNION ALL` combine the results of two or more `SELECT` statements. However, `UNION` removes duplicate rows, while `UNION ALL` includes all rows, including duplicates.
*   **How can you retrieve matching and non-matching records from two tables?**

    You can retrieve matching and non-matching records from two tables using a **FULL OUTER JOIN**. The `FULL OUTER JOIN` keyword returns all rows from both tables involved in the join, regardless of whether they have a matching row in the other table. In cases where a row from one table does not have a match in the other table, the columns from the table without a match will contain `NULL` values. This ensures that no rows are excluded from the final result set.
*   **Explain how to join more than two tables.**

    You can join more than two tables by using multiple join clauses in a single query. For example:

    ```sql
    SELECT *
    FROM Customers c
    INNER JOIN Orders o ON c.CustomerID = o.CustomerID
    INNER JOIN OrderDetails od ON o.OrderID = od.OrderID;
    ```
*   **What is the importance of the ON clause in a JOIN?**

    The `ON` clause in a `JOIN` specifies the condition that determines which rows from the tables are joined. It is important because it defines the relationship between the tables being joined.
*   **How do you handle null values when performing joins?**

    Null values require special handling when performing joins because a comparison involving `NULL` always evaluates to **unknown**, not true or false. This means that rows with `NULL` values in the joining columns may not be included in the join result unless explicitly handled.

    You can handle null values when performing joins using the `IS NULL` and `IS NOT NULL` operators in the `ON` clause or the `WHERE` clause to explicitly include or exclude rows with `NULL` values in the joining columns. For example:

    ```sql
    SELECT c.CustomerID, o.OrderID
    FROM Customers c
    LEFT JOIN Orders o ON c.CustomerID = o.CustomerID
    WHERE o.CustomerID IS NULL;
    ```

### Subqueries

*   **What is a subquery in SQL?**

    A **subquery** is a query nested inside another query. The outer query is called the main query, while the inner query is the subquery. Subqueries can return a single value, a list of values, or even a complete result set. 
*   **How do you use a subquery in a WHERE clause?**

    A subquery in a `WHERE` clause can fetch data that will be used for filtering in the main query. The main query can then use operators like `IN`, `NOT IN`, `ANY`, `ALL`, or comparison operators (>, <, =, etc.) to compare its values with the results returned by the subquery.

    For example, to find all customers who have placed orders:

    ```sql
    SELECT *
    FROM Customers
    WHERE CustomerID IN (SELECT DISTINCT CustomerID FROM Orders);
    ```
*   **Can you explain the difference between a correlated and a non-correlated subquery?**

    *   **Correlated Subquery:** A correlated subquery depends on the outer query for its values, meaning it references columns from the outer query. It executes once for each row returned by the outer query.

    *   **Non-Correlated Subquery:** A non-correlated subquery can execute independently of the main query and returns a value that is then used by the main query. It executes only once for the entire main query.

        The example provided for "How do you use a subquery in a `WHERE` clause" is an example of a non-correlated subquery.

        Here is an example of a correlated subquery:

        ```sql
        SELECT *
        FROM Orders o
        WHERE o.OrderID = (SELECT MAX(OrderID) FROM Orders WHERE CustomerID = o.CustomerID);
        ```
*   **How can you return multiple values from a subquery?**

    You can return multiple values from a subquery by using the `IN` operator or by using the subquery as a derived table. For example, using the `IN` operator:

    ```sql
    SELECT *
    FROM Customers
    WHERE CustomerID IN (SELECT CustomerID FROM Orders WHERE OrderDate = '2023-03-01');
    ```
*   **Explain the use of subqueries in the SELECT clause.**

    A subquery in the `SELECT` clause can be used to retrieve data that is not directly present in the tables used in the main query. The subquery acts as a separate query that computes a value for each row returned by the main query.

    For example, to retrieve the customer name and their latest order date:

    ```sql
    SELECT 
        c.CustomerName,
        (SELECT MAX(o.OrderDate) FROM Orders o WHERE o.CustomerID = c.CustomerID) as LatestOrderDate
    FROM Customers c;
    ```
*   **What are scalar subqueries and how are they used?**

    A scalar subquery is a subquery that returns a single value. Scalar subqueries can be used in various parts of a SQL query, including the `SELECT`, `WHERE`, and `HAVING` clauses, to retrieve a single value based on a condition or calculation. 

    For example, to get all customers who live in the same city as the customer with CustomerID 1:

    ```sql
    SELECT *
    FROM Customers
    WHERE City = (SELECT City FROM Customers WHERE CustomerID = 1);
    ```
*   **How do you perform a DELETE operation using a subquery?**

    To delete records from a table based on conditions from another table, you can use a subquery with the `DELETE` statement. The subquery identifies the target rows to be removed from the table. 

    For example, to delete all orders from customers who have the 'Closed' status:

    ```sql
    DELETE FROM Orders
    WHERE CustomerID IN (SELECT CustomerID FROM Customers WHERE CustomerStatus = 'Closed');
    ```
*   **What are the limitations of subqueries?**

    *   **Performance:** Subqueries can sometimes lead to performance issues, especially correlated subqueries that execute for each row of the outer query.
    *   **Readability:** Complex subqueries can make queries harder to read and understand.
    *   **Limited Functionality:** Subqueries may not be supported in all database systems or may have limitations in terms of the operations that can be performed within them.
*   **Can subqueries be used with JOIN? How?**

    Yes, subqueries can be used with joins. A subquery can be used in the `FROM` clause of a query to create a temporary table-like structure, known as a derived table or inline view, which can then be joined with other tables using the `JOIN` clause.

    For example, to join a table with a subquery:

    ```sql
    SELECT c.CustomerID, s.MaxOrderDate
    FROM Customers c
    JOIN (SELECT CustomerID, MAX(OrderDate) as MaxOrderDate FROM Orders GROUP BY CustomerID) s
    ON c.CustomerID = s.CustomerID;
    ```

### Indexes

*   **What is an index in SQL?**

    An index is a data structure that improves the speed of data retrieval operations on a database table. It does this by creating a separate structure that contains a portion of the table's data, like a specific column or a combination of columns, and a pointer to the actual row in the table where the complete data resides. This allows the database to quickly locate the desired data based on the indexed column values without having to scan the entire table.
*   **How do indexes improve query performance?**

    Indexes improve query performance by allowing the database to quickly locate the rows that match the search criteria without having to scan the entire table. Instead of scanning every row, the database uses the index to directly access only the relevant rows, significantly reducing the number of disk I/O operations and speeding up data retrieval.
*   **Explain the difference between a clustered and a non-clustered index.**

    *   **Clustered index:** Defines the physical order in which data is stored in a table. A table can have only one clustered index, and it significantly impacts the performance of queries that retrieve data based on the indexed column or a range of values.

    *   **Non-clustered index:** Created on one or more columns of a table but doesn't define the physical order of the data. A table can have multiple non-clustered indexes.
*   **How do you create an index on a table?**

    You can create an index on a table using the `CREATE INDEX` statement. For example:

    ```sql
    CREATE INDEX IX_Customers_City
    ON Customers (City);
    ```
*   **What are the advantages and disadvantages of using indexes?**

    **Advantages:**

    *   Faster data retrieval
    *   Improved query performance
    *   Enhanced search capabilities

    **Disadvantages:**

    *   Additional storage space required
    *   Increased overhead for data modification operations (insert, update, delete)
    *   Can slow down write operations

*   **How can you check if an index is being used in a query?**

    You can check if an index is being used in a query using the query execution plan or explain plan provided by the database system. The execution plan shows the steps involved in executing a query, including the indexes used, join operations, and other optimization strategies.
*   **Explain the concept of composite indexes.**

    A composite index, also known as a multi-column index, is an index that is created on two or more columns of a table. The order of the columns in the index definition matters, as it determines the index's effectiveness for different query conditions.
*   **How does indexing affect INSERT, UPDATE, and DELETE operations?**

    While indexes speed up `SELECT` queries, they can slow down `INSERT`, `UPDATE`, and `DELETE` operations because the index needs to be updated every time data in the indexed column(s) changes. This means additional overhead for maintaining the index, potentially impacting the performance of these data modification operations. 
*   **When should you avoid using indexes?**

    *   Small tables with limited data: Indexes may not provide significant performance benefits for small tables because scanning the entire table may be faster than using an index.
    *   Columns that are frequently updated:
    *   Tables with high insert, update, or delete operations: As mentioned earlier, indexes can slow down data modification operations.

*   **How do you remove an index from a table?**

    You can remove an index from a table using the `DROP INDEX` statement. For example:

    ```sql
    DROP INDEX IX_Customers_City;
    ```

### Transactions

*   **What is a transaction in SQL?**

    A transaction in SQL is a sequence of one or more SQL statements that are treated as a single unit of work. This means that all statements within a transaction are executed successfully for the changes to be permanently saved in the database. If any statement within the transaction fails, all changes made within the transaction are rolled back to the initial state, ensuring data consistency and integrity. 
*   **Explain the ACID properties of a transaction.**

    The ACID properties of a transaction are:

    *   **Atomicity:**  A transaction is treated as a single unit of work, either all of its changes are applied to the database, or none of them are. 
    *   **Consistency:** Ensures that a transaction brings the database from one valid state to another, preserving the integrity of the data. 
    *   **Isolation:** Transactions are isolated from each other, meaning that changes made within one transaction are not visible to other transactions until the transaction is committed. 
    *   **Durability:** Once a transaction is committed, its changes are permanently saved in the database, even in the event of system failures. 
*   **How do you start and end a transaction?**

    You can start a transaction using the `BEGIN TRANSACTION` statement and end a transaction using either the `COMMIT` statement (to save the changes) or the `ROLLBACK` statement (to undo the changes). For example:

    ```sql
    BEGIN TRANSACTION;
    -- SQL statements to be executed within the transaction
    COMMIT; -- Or ROLLBACK; to undo changes
    ```
*   **What is the purpose of the COMMIT and ROLLBACK commands?**

    *   **COMMIT:** Used to permanently save the changes made within a transaction to the database. Once a transaction is committed, the changes are made visible to other transactions and are durable, meaning they will persist even in case of system failures.

    *   **ROLLBACK:** Used to undo the changes made within a transaction. If any statement within the transaction fails or if the user explicitly issues a `ROLLBACK` command, all changes made since the beginning of the transaction are undone, restoring the database to its state before the transaction started.
*   **How can you ensure data consistency in transactions?**

    You can ensure data consistency in transactions by adhering to the ACID properties, using appropriate transaction isolation levels, and implementing error handling and rollback mechanisms to handle potential failures.
*   **Explain the concept of transaction isolation levels.**

    Transaction isolation levels control the degree to which transactions are isolated from each other, determining how and when changes made by one transaction are visible to other concurrent transactions. Different isolation levels provide varying levels of protection against concurrency-related issues like dirty reads, non-repeatable reads, and phantom reads. The standard SQL isolation levels are:

    *   **Read Uncommitted:** Allows transactions to read data that has been modified by other transactions but not yet committed. 
    *   **Read Committed:** Ensures that transactions only read committed data, preventing dirty reads, but still allowing non-repeatable reads.
    *   **Repeatable Read:** Guarantees that a transaction will read the same data multiple times within the transaction, even if other transactions make changes. 
    *   **Serializable:** Provides the highest level of isolation, ensuring that transactions are executed in a serializable manner as if they were executed one after the other, preventing most concurrency-related issues.

*   **What is a deadlock and how do you prevent it in transactions?**

    A deadlock is a situation in which two or more transactions are blocked indefinitely, each holding a resource that the other transaction needs to proceed.  

    **Deadlock Prevention Techniques:**

    *   **Lock Timeouts:** Implementing lock timeouts ensures that transactions are automatically released after a certain period of time, preventing deadlocks that occur due to long-running transactions. 
    *   **Deadlock Detection and Resolution:** Database systems often have built-in mechanisms to detect and resolve deadlocks. When a deadlock is detected, the database system typically chooses one of the transactions involved as the victim and rolls back that transaction, allowing other transactions to proceed.
*   **How can you implement a save point in a transaction?**

    A savepoint in a transaction allows you to mark an intermediate point within the transaction to which you can roll back later. If an error occurs after the savepoint, you can choose to roll back to the savepoint instead of rolling back the entire transaction.

    You can implement a savepoint using the `SAVEPOINT` statement. For example:

    ```sql
    BEGIN TRANSACTION;
    -- SQL statements
    SAVEPOINT Savepoint1;
    -- More SQL statements
    -- If an error occurs here, you can roll back to Savepoint1
    ROLLBACK TO Savepoint1;
    -- Or COMMIT to commit the entire transaction
    COMMIT;
    ```
*   **What is the difference between explicit and implicit transactions?**

    *   **Explicit Transaction:**  A transaction that is explicitly started by the user using transaction control statements like `BEGIN TRANSACTION`, `COMMIT`, and `ROLLBACK`.

    *   **Implicit Transaction:** A transaction that is automatically started by the database system when a DML (Data Manipulation Language) statement like `INSERT`, `UPDATE`, or `DELETE` is executed without an explicit transaction block. 
*   **How do transactions work in a distributed database environment?**

    Transactions in a distributed database environment involving multiple databases or servers introduce complexities to ensure atomicity, consistency, isolation, and durability across all participating systems. This is where distributed transaction management systems come into play. These systems coordinate transactions across multiple database servers to maintain data integrity and consistency. One common approach is the **two-phase commit** protocol.

### Stored Procedures and Functions

*   **What is a stored procedure in SQL?**

    A stored procedure is a precompiled collection of one or more SQL statements that can be executed as a unit, stored and executed on the database server, offering advantages like reusability, security, and performance improvements.
*   **How do stored procedures differ from functions?**

    | Feature              | Stored Procedure                          | Function                               |
    | :-------------------- | :---------------------------------------- | :------------------------------------- |
    | **Return Value**     | Can return zero or multiple values      | Always returns a single value           |
    | **Data Modification** | Can modify data in tables                 | Primarily used to compute and return a value |
    | **Execution Context** | Executed in its own execution context    | Can be called within SQL statements    |
*   **How do you create a stored procedure in SQL?**

    The syntax for creating stored procedures may vary slightly depending on the database system being used. Here is an example of creating a stored procedure in MySQL:

    ```sql
    DELIMITER //
    CREATE PROCEDURE GetCustomerOrders (IN CustomerID INT)
    BEGIN
        SELECT * FROM Orders WHERE CustomerID = CustomerID;
    END //
    DELIMITER ;
    ```
*   **What are the advantages of using stored procedures?**

    *   **Reusability:** Stored procedures can be reused by multiple applications or users, reducing code duplication and promoting consistency in data access. 
    *   **Security:** Offer a way to control access to sensitive data and operations. You can grant permissions to users or applications to execute stored procedures without giving them direct access to the underlying tables or data.
    *   **Reduced Network Traffic:**  Help reduce network traffic because instead of sending multiple SQL statements, only the stored procedure call is sent over the network.
    *   **Improved Performance:** Precompiled and optimized for execution, reducing the overhead of query parsing and optimization each time they are executed.
*   **How do you pass parameters to a stored procedure?**

    You can pass parameters to a stored procedure by enclosing them in parentheses after the stored procedure's name. For example:

    ```sql
    CALL GetCustomerOrders(1);
    ```
*   **Explain the difference between input and output parameters in stored procedures.**

    *   **Input Parameters:** Used to pass values from the calling program or query to the stored procedure.

    *   **Output Parameters:**  Used to return values from the stored procedure to the calling program or query.
*   **How do you handle exceptions in a stored procedure?**

    Exceptions in stored procedures can be handled using try-catch blocks in some database systems.  For example, in SQL Server:

    ```sql
    CREATE PROCEDURE ExampleProcedure
    AS
    BEGIN
        BEGIN TRY
            -- SQL statements that may cause an exception
        END TRY
        BEGIN CATCH
            -- Exception handling logic
        END CATCH
    END;
    ```
*   **Can you call a stored procedure within another stored procedure?**

    Yes, you can call a stored procedure within another stored procedure. This is known as a nested stored procedure call. The inner stored procedure will execute within the context of the outer stored procedure, and any changes made by the inner stored procedure will be visible to the outer stored procedure.
*   **How do you create and use a user-defined function in SQL?**

    A user-defined function (UDF) in SQL is a database object that encapsulates a block of SQL code, allowing you to extend the functionality of SQL by creating your own custom functions. UDFs can return scalar values (single values) or tables (result sets).

    To create a user-defined function, you use the `CREATE FUNCTION` statement. The syntax for creating UDFs varies slightly depending on the specific database system.

    Here is an example of creating a scalar UDF in SQL Server that calculates the discount amount based on the product price and a discount percentage:

    ```sql
    CREATE FUNCTION CalculateDiscount (
        @Price DECIMAL(10,2),
        @DiscountPercentage DECIMAL(5,2)
    )
    RETURNS DECIMAL(10,2)
    AS
    BEGIN
        DECLARE @DiscountAmount DECIMAL(10,2);
        SET @DiscountAmount = @Price * (@DiscountPercentage / 100);
        RETURN @DiscountAmount;
    END;
    ```
*   **What are the limitations of stored procedures?**

    *   **Database Platform Dependency:** Typically tied to the specific database platform they were created for. This means that a stored procedure written for MySQL, for instance, may not be directly portable to another database system like SQL Server or Oracle without modifications.
    *   **Debugging and Testing:**  Can be more challenging to debug and test compared to code written in a general-purpose programming language because they often involve database-specific tools and techniques. 
    *   **Potential Performance Issues:** If not designed and optimized correctly, they can lead to performance issues, especially if they are complex or contain inefficient queries.

### Normalization and Database Design

*   **What is normalization in database design?**

    Normalization is the process of organizing data in a database to reduce data redundancy and improve data integrity. It involves dividing large tables into smaller, well-structured tables and defining relationships between them.
*   **Explain the different normal forms with examples.**

    *   **1NF (First Normal Form):**  A table is in 1NF if it contains only atomic values (indivisible values) in each column. This means that each column should hold a single value, and there should be no repeating groups of columns.

        **Example:** A table named "Employees" is in 1NF if it has separate columns for "EmployeeID," "FirstName," "LastName," "Address," etc., with each column holding a single value.
    *   **2NF (Second Normal Form):** A table is in 2NF if it is in 1NF and all non-key attributes (columns that are not part of the primary key) are fully dependent on the entire primary key, not just a part of it.

        **Example:**  Consider a table named "Orders" with columns "OrderID" (primary key), "ProductID," "Quantity," and "ProductName."  If "ProductName" depends only on "ProductID" and not on the entire "OrderID," it violates 2NF. To achieve 2NF, you would create a separate table for "Products" with "ProductID" and "ProductName."
    *   **3NF (Third Normal Form):** A table is in 3NF if it is in 2NF and all non-key attributes are not transitively dependent on the primary key. This means that non-key attributes should not depend on other non-key attributes, only on the primary key.

        **Example:** In a table named "Customers" with columns "CustomerID" (primary key), "CustomerName," "City," and "ZipCode,"  if "City" determines "ZipCode" (transitive dependency), it violates 3NF. To achieve 3NF, you would create a separate table for "Cities" with "City" and "ZipCode."

        Higher normal forms like Boyce-Codd Normal Form (BCNF) and Fourth Normal Form (4NF) address more specific data redundancy scenarios. 
*   **What is denormalization and when is it used?**

    Denormalization is the process of intentionally introducing some degree of redundancy into a database design to improve the performance of certain queries. It is typically done by adding redundant data to tables that are frequently queried together, reducing the need for complex joins and improving query response times.

    **When to Use Denormalization:**

    *   **Read-Heavy Workloads:** When the database is primarily used for read operations (SELECT queries) and write operations are infrequent, denormalization can improve read performance.
    *   **Reporting and Analytical Queries:** For reporting and analytical queries that involve large datasets and complex joins, denormalization can simplify the queries and reduce execution time.
*   **How do you handle many-to-many relationships in database design?**

    A many-to-many relationship in a database design occurs when multiple records in one table can be associated with multiple records in another table, and vice versa.  To represent many-to-many relationships in a relational database, you typically use an intermediary table, often referred to as a **junction table** or **associative table**. 

    **Example:** Consider a scenario with two tables: "Students" and "Courses." A student can enroll in multiple courses, and a course can have multiple students. In this case, you would create a junction table named "Enrollments" with columns like "EnrollmentID," "StudentID," and "CourseID," linking the two tables.
*   **What is a primary key and why is it important?**

    A primary key is a column or set of columns in a table that uniquely identifies each row in that table. It enforces entity integrity, ensuring that each row in the table can be uniquely identified, preventing duplicate records and providing a way to reference specific rows from other tables using foreign keys.
*   **Explain the concept of foreign keys and referential integrity.**

    A foreign key is a column or set of columns in one table that refers to the primary key of another table. It establishes a link between the data in two tables, enforcing referential integrity.

    Referential integrity ensures that relationships between tables are maintained consistently. It prevents actions that would destroy the link between tables, such as deleting a record in the parent table (the table with the primary key) that has related records in the child table (the table with the foreign key).
*   **How do you design a database schema for a new application?**

    **Steps to Design a Database Schema:**

    1.  **Requirements Gathering and Analysis:** Start by thoroughly understanding the application's requirements, including the data to be stored, the relationships between data entities, and the operations that will be performed on the data.

    2.  **Conceptual Data Modeling:** Create a conceptual data model, such as an Entity-Relationship Diagram (ERD), to visually represent the entities, attributes, and relationships within the database.

    3.  **Logical Data Modeling:**  Translate the conceptual data model into a logical data model, defining tables, columns, data types, primary keys, and foreign keys.

    4.  **Normalization:** Apply normalization rules to the logical data model to minimize data redundancy and ensure data integrity.

    5.  **Physical Database Design:** Determine the physical storage parameters for the database, such as filegroups, indexes, and storage space allocation.

    6.  **Implementation:** Implement the physical database design by creating the database objects (tables, indexes, etc.) using SQL scripts or database management tools.
*   **What are the common pitfalls in database design?**

    *   **Inadequate Requirements Gathering:**  Failing to thoroughly gather and analyze requirements can lead to a database design that does not meet the application's needs.
    *   **Poor Normalization:** Incorrect or insufficient normalization can result in data redundancy, update anomalies, and data integrity issues.
    *   **Lack of Indexing:**  Without proper indexing, queries can become slow and inefficient, impacting application performance. 
    *   **Ignoring Data Integrity Constraints:** Neglecting data integrity constraints can lead to inconsistent or invalid data in the database.
*   **How do you ensure scalability in a database design?**

    **Techniques to Ensure Database Scalability:**

    *   **Database Sharding:** Involves horizontally partitioning the database into multiple smaller databases (shards) distributed across multiple servers.
    *   **Replication:** Creating replicas (copies) of the database on multiple servers. Replication improves read performance and provides high availability.
    *   **Caching:**  Storing frequently accessed data in a cache to reduce the load on the database server.
*   **What is the importance of indexing in database design?**

    Indexing plays a critical role in database design by significantly improving the performance of data retrieval operations (SELECT queries), allowing databases to quickly locate the desired data without performing full table scans. Indexes enhance search capabilities and are especially important for tables with a large number of rows or frequently queried columns. However, it's essential to strike a balance, as indexes can introduce overhead for write operations (INSERT, UPDATE, DELETE), and having too many indexes can negatively impact write performance.
