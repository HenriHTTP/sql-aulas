 
 # Introduction to databases
 ***
A database is a structured collection of information or data stored in a computer system. It is designed to efficiently organize, manage, and retrieve data. Databases are used to store and access various types of data, such as customer information, product details, or records, making it easier to search, update, and analyze the information as needed. To interact with databases, businesses and individuals rely on **Database Management Systems **(DBMS), which are specialized software applications responsible for managing and controlling access to the database. DBMS provides tools and features for creating, modifying, and querying the data in a secure and organized manner, ensuring data integrity and enabling multiple users to work with the data simultaneously while maintaining consistency and security

 ## Database type

- Document-oriented, COBOL (IMS,IDMS)
- Relational (SQL ,DB 2,Oracle)
- Object Oriented (Old PostgreSQL)
- NoSQL (MongoDB)

***
# Transaction

Transactions are operations performed on a database that take the database from one consistent state to another consistent one.They are used to ensure the integrity and consistency of data in a relational database, following the ACID concept 
## Transaction types

- **Commit** :These are operations that, after commit, changes become permanent and visible to other users

```sql
-- inital this transition
BEGIN TRANSACTION; 

-- starting operations read values in colums
UPDATE tables SET columns= values_ WHERE condiction;

-- starting operations insert values in colums
INSERT INTO tables (colum1, colum2) VALUES (value1, value2);

-- Commit operation
COMMIT;

```

- **Rollback**: This will revert all changes made to the transaction to the state before the transaction.

```sql
-- inital this transition
BEGIN TRANSACTION;

-- starting operations read values in colums
UPDATE tables SET columns = values_ WHERE condiction;

-- err or condition require rollback

 -- Return transition not commit
ROLLBACK;

```

- **Savepoint** : is a markup within a transaction that allows you to return to a specific point within the transaction.

```sql
BEGIN TRANSACTION;
-- Perform some update operations
SAVEPOINT my_savepoint; -- Create a savepoint
-- More update operations
-- Something goes wrong, and you decide to roll back to the savepoint
ROLLBACK TO my_savepoint; -- Return to the savepoint
-- Continue with the remaining operations
COMMIT;

```

- **Autocommit**: not's  require command  **COMMIT** and  **BEGIN TRANSACTION** for starting a new transaction 

```sql
-- Autocommit is enabled by default
-- Each statement is a transaction
INSERT INTO table_ (column) VALUES (value1);
UPDATE table SET column = value2 WHERE condition;
-- Changes are automatically committed

```


***
 
 # ACID
 
 in computer science, **ACID** (atomicity, consistency, isolation, durability) is a set of properties of database transactions intended to guarantee data validity.
 
- ** Atomicity** : if something operation return error all operation will return rollback.

```sql
-- inital this transition
BEGIN TRANSACTION;
 
-- insert value in there database
INSERT INTO table_ (atribute) VALUES (true);
  
-- insert value invalid in table retun error
UPDATE tb SET atribute=false WHERE atribute=false

--commits should not be made
COMMIT;
````

-  **Consistency** : if the foreign key has no reference, data should not be inserted and should not query completed.

``` sql 
--inital this transiton
BEGIN TRANSACTION;

-- insert new user in the table
INSERT INTO table_ (user_id, name_) VALUES (1, 'name');

-- insert new orders for client id "1"
INSERT INTO Orders (order_id, customer_id, order_total) VALUES (101, 1, 500.00);

-- value invalid because id "2" not exits
INSERT INTO Orders (order_id, customer_id, order_total) VALUES (102, 2, 300.00);

--commits should not be made
COMMIT;
```
 
- ** Isolation** : if multiple users are trying to access a database and perform multiple transactions, should the database perform parallel transactions for each user after a commit.

```sql
-- Set the isolation level to READ UNCOMMITTED

-- READ UNCOMMITTED: 
/* 
In this isolation level, 
T1 can read uncommitted changes made by T2,
and T2 can read uncommitted changes made by T1
*/

SET SESSION TRANSACTION ISOLATION LEVEL READ UNCOMMITTED;
-- Start transaction T1
START TRANSACTION;

-- T1 transfers $500 from Account 1 to Account 2
UPDATE Accounts SET Balance = Balance - 500 WHERE Number = 1;
UPDATE Accounts SET Balance = Balance + 500 WHERE Number = 2;

-- Start transaction T2
START TRANSACTION;

-- T2 checks the balance of Account 1
SELECT Balance FROM Accounts WHERE Number = 1;

-- Commit transaction T1
COMMIT;

-- Commit transaction T2
COMMIT;
```

```sql

-- Set the isolation level to READ COMMITTED
-- READ COMMITTED: 
/* 
In this isolation level,
transactions can only read committed changes 
made by other transactions. 
*/

SET SESSION TRANSACTION ISOLATION LEVEL READ COMMITTED;

-- Start transaction T1
START TRANSACTION;

-- T1 transfers $500 from Account 1 to Account 2
UPDATE Accounts SET Balance = Balance - 500 WHERE Number = 1;
UPDATE Accounts SET Balance = Balance + 500 WHERE Number = 2;

-- Start transaction T2
START TRANSACTION;

-- T2 checks the balance of Account 1
SELECT Balance FROM Accounts WHERE Number = 1;

-- Commit transaction T1
COMMIT;

-- Commit transaction T2
COMMIT;
```

- **Durability**:  ever data should percist in database after commit
 
```sql
-- inital this transition
BEGIN TRANSACTION;
 
-- insert value in there database
INSERT INTO table_ (atribute_) VALUES (values_);
  
--commits values
COMMIT;
```

***

# ANSI / SPARC

The **ANSI-SPARC Architecture** (American National Standards Institute, Standards Planning And Requirements Committee), is an abstract design standard for a database management system (DBMS), first proposed in 1975.



![image](./ANSI-SPARC_DB_model.jpg)
- **External level (view)** :  Inside the "External level"  layer, you'll find the interface, software, and access restrictions for the end user.
- **Conceitual level (Schema)** : inside the "Conceitual level" , you'll find tables , sql query, source code  for developer.
- **Intenal level(DBMS)** : nside the "internal level" , you'll find DBMS and archive system in core
***

# Restrictions

- **Domain** : Values types (**null, interger , string , boolean**).
- **Reference** :  the data has should **Consistency**
- **User**: user **business rules**
***