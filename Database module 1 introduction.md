 ***
 
 #### Database type

- Document-oriented, COBOL (IMS,IDMS)
- Relational (SQL ,DB 2,Oracle)
- Object Oriented (Old PostgreSQL)
- NoSQL (MongoDB)

***

 #### ACID
 
- Atomicity: if something operation return error all operation will return rollback

```sql
-- inital transition
BEGIN TRANSACTION;
 
-- insert value in there database
INSERT INTO table_ (atribute) VALUES (true);
  
-- insert value invalid in table retun error
UPDATE tb SET atribute=false WHERE atribute=false

--commits should not be made
COMMIT;
````

- Consistency : if the foreign key has no reference, data should not be inserted and should not query completed

``` sql 
--inital transiton
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
 
- Isolation :

```sql
```

