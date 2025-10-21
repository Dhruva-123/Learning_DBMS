
This is a way to store data. A server is hosted and the server gives out the SQL file to the users that are authorized to access it. We can add or remove users of each server so our data is private to the given list of users. We can also restrict the user to have read or write or both privilages depending upon the standing of the user. This is a full form data storage language. Each DB created will be stored inside a particular folder in our PC locally and we cannot store that data anywhere we want. In order to import or export data from PC to other sources, we need to create a '.sql' file and then export that file. Once exported, the party wanting to use that given .sql file needs to open that file inside their sql workbench of other workable enviornment and that will give them full freedom over the data. Once opened, the matadata is saved locally in their PC in the exact same file every other DB is going to. This is the concept of SQL and how it is handled. Now, to get to the code of SQL.


## SQL concepts

- In order to create databases, we use the simple syntax;

		CREATE DATABASE name_of_the_database;

The semi colon is a must and tells the SQL framework where exactly the line ends.

- Here, We need to specify which database we are using in the list of databases. Therefore, we use the syntax;

		 USE name_of_the_database;
This syntax is pretty straight forward. Moving forward, every change we make will be in the selected database.

- We can drop entire databases with the single line;
			`DROP DATABASE name_of_the_database;
This deletes the entire database. 


- In order to make your database read only and immutable, you use this command;
		`` ALTER DATABASE name_of_the_database READ ONLY = 1;

of course, when the read-only is set to 1, the database cannot be changed. It will remain read - only.
This, I assume, will be useful once the entire database is cleanly updated and ready for other purposes. 

NOTE: When I say a database is immutable, it cannot be deleted aswell. To disable read-only, we just set it equal to 0.

- To create a table, we first need to 'USE' the required database and then, we use the create table command as follows;
		`CREATE TABLE NAME_OF_THE_TABLE (different column names seperated by commas);
EX:
CREATE TABLE Empolyee_data(Name datatype, ID datatype, Email datatype, Pay datatype, date of joining datatype etc etc);
Note that we do not use the "" marks for column names because we are creating objects and variables there, we are not passing a string. We are naming a string. For each column, we must specify the datatype we are going to store inside it. The datatypes go as follows:

| Type              | Storage | Range          | Notes                                                 |
| ----------------- | ------- | -------------- | ----------------------------------------------------- |
| `TINYINT`         | 1 byte  | -128 to 127    | Great for boolean flags (`is_active`, `status_code`). |
| `SMALLINT`        | 2 bytes | ±32K           | Compact for small counts, like age, quantity.         |
| `MEDIUMINT`       | 3 bytes | ±8M            | Rarely used — middle ground.                          |
| `INT` / `INTEGER` | 4 bytes | ±2B            | Standard default choice for IDs.                      |
| `BIGINT`          | 8 bytes | ±9 quintillion | Use for large-scale datasets or global counters.      |
|                   |         |                |                                                       |

| Type            | Use Case                | Precision  | Notes                                                        |
| --------------- | ----------------------- | ---------- | ------------------------------------------------------------ |
| `DECIMAL(p, s)` | Money, accounting       | Exact      | Stores as string internally, prevents float rounding issues. |
| `FLOAT`         | Scientific data         | ~7 digits  | Faster but imprecise.                                        |
| `DOUBLE`        | Scientific, ML datasets | ~15 digits | Use when you need precision but not exactness.               |
|                 |                         |            |                                                              |

| Type        | Format                | Notes                                            |
| ----------- | --------------------- | ------------------------------------------------ |
| `DATE`      | `YYYY-MM-DD`          | For birthdates, logs, etc.                       |
| `DATETIME`  | `YYYY-MM-DD HH:MM:SS` | No timezone; used for general timestamps.        |
| `TIMESTAMP` | `YYYY-MM-DD HH:MM:SS` | Auto converts to UTC; smaller range (1970–2038). |
| `TIME`      | `HH:MM:SS`            | Duration or clock time.                          |
| `YEAR`      | `YYYY`                | Rarely used; avoid for future-proofing.          |

| Type         | Max Length    | Notes                                                   |
| ------------ | ------------- | ------------------------------------------------------- |
| `CHAR(n)`    | Fixed         | Faster for fixed-length codes (ISO codes, hashes).      |
| `VARCHAR(n)` | Variable      | Most common. Size limit ~65K per row.                   |
| `TEXT`       | 65,535 chars  | For long text (e.g., descriptions).                     |
| `MEDIUMTEXT` | 16 MB         | Large articles.                                         |
| `LONGTEXT`   | 4 GB          | Rarely needed; think logs or blobbed JSON.              |
| `ENUM`       | 1–255 options | Efficient categorical field, but not easily extensible. |

|Type|Size|Use|
|---|---|---|
|`BLOB`|64 KB|Binary data — files, images, etc.|
|`MEDIUMBLOB`|16 MB|Larger binaries.|
|`LONGBLOB`|4 GB|Huge files.|

|Type|Notes|
|---|---|
|`BOOLEAN` / `BOOL`|Alias for `TINYINT(1)` — stores 0/1.|
|`BIT(n)`|Bit-field storage, rarely used except for flags.|


of all these data types, the most important ones we use are, VARCHAR(n), text, bool, int, Datetime ETC. Also note that in decimal, the first argument is the total number of digits possible in the given datatype and the second argument is the precision (number of digits after the decimal).

- In order to see or 'select' data from a given table, we use the keyword select and it goes as follows;
			`SELECT * FROM NAME_OF_THE_TABLE;

As we know, * represents everything. That means, we are selecting everything from the given table. But if we do not want that, we can type the name of a particular column and then select it. Selecting any data inside a table let's us see what's in the table.

If we want a countable number of columns, we can use this syntax;

			SELECT col1, col2, ... etc FROM NAME_OF_THE_TABLE;

- Of course we can rename the entire table with just the keyword "rename" and that goes something like this:
		`RENAME TABLE former_name TO later_name;
This only works for a table though, not the entire database.

- Here comes one of the most important keywords in the entire SQL language. 
- The keyword 'ALTER' functions in a lot of different ways. It is used to add columns to a table, remove columns from a table, etc etc. Here is a single use case;
				`ALTER TABLE name_of_the_table 
				whatever alteration you want;

Note that the alter statement itself doesn't have any semi colon to it simply because that itself is not the end of the command. 

Here is a dump of where and how the keyword "Alter" is useful

### 🧱 1. `ALTER TABLE`

This is where 90% of `ALTER` usage happens.

#### ✅ You Can:

- **Add / Drop Columns**
    
    `ALTER TABLE employees ADD COLUMN age INT; ALTER TABLE employees DROP COLUMN salary;`
    
- **Modify Column Datatype / Default**
    
    `ALTER TABLE employees MODIFY COLUMN age SMALLINT; ALTER TABLE employees ALTER COLUMN age INT DEFAULT 18;
    
- **Rename Columns**
    
    `ALTER TABLE employees RENAME COLUMN age TO employee_age;`
    
- **Rename the Table**
    
    `ALTER TABLE employees RENAME TO staff;`
    
- **Add / Drop Constraints**
    
    `ALTER TABLE employees ADD CONSTRAINT pk_emp PRIMARY KEY (id); ALTER TABLE employees DROP CONSTRAINT pk_emp;`
    
- **Add / Drop Indexes**
    
    `ALTER TABLE employees ADD INDEX idx_name (name); ALTER TABLE employees DROP INDEX idx_name;`
    
- **Add / Drop Foreign Keys**
    
    `ALTER TABLE orders ADD FOREIGN KEY (emp_id) REFERENCES employees(id);`
    
- **Change Storage Engine or Character Set**
    
    `ALTER TABLE employees ENGINE = InnoDB; ALTER TABLE employees CONVERT TO CHARACTER SET utf8mb4;`
    

💡 **Strategic note:**  
`ALTER TABLE` locks the table while operating — on large datasets this can freeze production.  
In big companies, DBAs use _online schema migration tools_ (like `gh-ost`, `pt-online-schema-change`) to make such changes safely.

---

### ⚙️ 2. `ALTER DATABASE`

Much smaller scope.

#### ✅ You Can:

- Change **character set** or **collation**:
    
    `ALTER DATABASE mydb CHARACTER SET = utf8mb4 COLLATE = utf8mb4_unicode_ci;`
    

#### 🚫 You Cannot:

- Rename the database
    
- Move or clone it
    
- Alter its user grants
    

So `ALTER DATABASE` is mostly for _text encoding and sorting rules_, not structural transformations.

---

### 🔐 3. `ALTER USER`

Used for authentication-level changes.

`ALTER USER 'rahul'@'localhost' IDENTIFIED BY 'NewPassword123';`

Or modify privileges and plugin auths.

---

### 🧠 4. `ALTER VIEW`

Change a view definition:

`ALTER VIEW active_employees AS SELECT * FROM employees WHERE is_active = 1;`

Equivalent to dropping and recreating, but keeps permissions.

---

### 🏗️ 5. `ALTER PROCEDURE`, `ALTER FUNCTION`, `ALTER EVENT`

Used to modify metadata (like SQL security or comments) —  
but you **can’t** actually edit their core logic; you must drop & recreate them.

---

### ALTER

|Level|What You Can Do|Risks|
|---|---|---|
|**Database**|Change encoding, defaults|Minimal|
|**Table**|Full schema mutation|Can lock or corrupt data if mishandled|
|**Column**|Change type, name, constraints|Data loss if conversion fails|
|**User**|Security and auth|Risk of lockout|
|**View/Procedure**|Update logic or permissions|Low, but can break dependencies|

Now, that is the single most powerful command in the entireity of SQL.


### DELETE, DROP

DELETE is a keyword used to delete rows. The keyword is usually followed by "FROM" and then table name and then a condition on which the deletion should occur. 

EX:
	`DELETE FROM table1 WHERE age < 18;

DROP is a keyword to delete an entire table or even a database. Just type DROP, then TABLE or DATABASE and then the name of the database or table.

EX:
	`DROP TABLE table1;
	`DROP DATABASE apex_legends;
	

### Auto commit:

- **Autocommit ON:** Each SQL statement is immediately committed; failures affect only that statement.
    
- **Autocommit OFF:** Statements are grouped in a transaction; you must `COMMIT` or `ROLLBACK`, so failures can undo all changes in the group.

			SET AUTOCOMMIT = 0; --> TURNED OFF
			SET AUTOCOMMIT = 1; --> TURNED ON

without autocommit, you would have to manually commit everything with a single worded line --> COMMIT;

to rollback : --> ROLLBACK; (Note that this only works before we commit, therefore, be careful when you commit if you actually plan on commiting)

By default, it's turned on.
There is a major disadvantage to using autocommit though. Once a line is run, it autocommits, so we cannot roleback if we want. But if we are commiting manually, we can always rollback.


### INSERT

In order to add rows to a particular table, first make sure that you are using that particular database and then do this:

				 INSERT INTO name_of_the_table VALUES
				 (row1),
				 (row2),
				 (row3);

However, say we don't have 10 rows of data for a particular row, but there are 10 columns, what we do is this:
				 ``` INSERT INTO name_of_the_table(column1, column2, column3) VALUES
				 (three_columns_data_row1),
				 (three_columns_data_row2);
				 ```


### 1. How to find the count of rows in a table?

In SQL, there are two ways to do this. One is rough and approximate, but very fast. The other is dependent on the size of the database. Usually we opt for the method which is O(n) because it is accurate and we don't use the O(1) method normally. 

#### O(n) method:

What we do here is, we make the computer check every row and make a count. Therefore, it is O(n). Here is the code for it:

`SELECT COUNT(*) FROM Schema_name.Table_name;`


#### O(1) method:

What we do here is, we go into the metadata of the table that we are querying from and we extract the count from there. This count refreshes only when the system auto ANALYSEs the data being pushed into it. The count we get will be from the last analysis. That count too is an estimate. therefore, we cannot really rely on this one to be exact. But it does give us an estimate real quick. Here is how you implement it:

`SELECT TABLE_ROWS FROM information_schema.tables WHERE table_schema = 'name_of_the_schema' AND table_name = 'name_of_the_table';`

NOTE: The `information_schema.tables` contains the metadata including, but not limited to, TABLE_ROWS, DATA_LENGTH, AVG_ROW_LENGTH, MAX_DATA_LENGTH, ENGINE, VERSION et cetera. 


### JOINS... What are they?


This table is all you need to know about joins:

| Join Type           | Set Analogy               | Explanation                                                            |
| ------------------- | ------------------------- | ---------------------------------------------------------------------- |
| **INNER JOIN**      | A ∩ B (intersection)      | Only rows that exist in both tables.                                   |
| **LEFT JOIN**       | A ∪ (A ∩ B complement)    | All rows from the left table; fill NULLs for missing right-table rows. |
| **RIGHT JOIN**      | B ∪ (B ∩ A complement)    | All rows from the right table; fill NULLs for missing left-table rows. |
| **FULL OUTER JOIN** | A ∪ B (union)             | All rows from both tables; fill NULLs where matches are missing.       |
| **CROSS JOIN**      | A × B (Cartesian product) | Every row from left combined with every row from right.                |

Left join basically does this:

whatever is in the left table must always be in the left join table. but, sometimes, the corresponding data related to the left table will not be in the right table. Then, we just add NULL to the columns related to the right table but we never leave the left table row. The number of rows in left join is EXACTLY equal to the number of rows in the left table. The same goes for right join.

Inner join only gives the particular row in the table if the entity we are basing our search on is in both the tables. Here are the code snippets of all the above joins in action.

#### INNER JOIN

`SELECT * FROM table_1 x INNER JOIN table_2 y ON x.ID = y.ID;`

What we are doing is, we are calling entities in table_1 as x and calling entities in table_2 as y. If for any entity x.ID = y.ID, then, it is quite clear that that particular row will be in the join. The x and y are solely used to write the condition. ON is the keyword, not where... ON.

#### LEFT JOIN

`SELECT * FROM table_1 x LEFT JOIN table_2 y ON x.ID = y.ID;`

I seriously do not think that right join is useful at all because we can just use left join on everything. So, I will not be writing the code here. It's a waste of space.

#### OUTER JOIN

`SELECT * FROM table_1 x OUTER JOIN table_2 y ON x.ID = y.ID;`

#### CROSS JOIN

`SELECT * FROM table_1 x CROSS JOIN table_2 y ON x.ID = y.ID;`


### How do you stack statements on one another?

```
SELECT COUNT(*) FROM (SELECT * FROM (SELECT x.*, y.amount, y.from_date, y.to_date FROM employee x LEFT JOIN salary y ON x.emp_no = y.emp_no AND y.to_date = '9999-01-01') as T WHERE amount IS NULL) AS k;
```
From that, we can clearly see that we are refining a table created and then seeing the number of rows in that table. All of this is stacked on one another. But the thing you'd notice is, we are using these two helping statements:

`as T` and `as K` .

Now, We did this because, wherever SQL expects a table, it doesn't take a statement. Take a look at this example:

`SELECT COUNT(*) FROM ...` SQL expects a table after that 'from'. We cannot give it a statement instead of a table. Therefore, we give it a statement and then name the statement as a variable T so that SQL thinks it's an actual table and runs the code inside. We are giving a fake variable to the whole statement. that's it.

### Sorting data

When we have a table and we want to view the table in a neat ascending order or descending order based on anything, this is what we need to do. We can either sort in ascending order or descending order. Both of their syntaxes are very similar so here is a snapshot of the code:

Ascending order:

`SELECT * FROM table_name ORDER BY column_name ASC;`

Descending order:

`SELECT * FROM table_name ORDER BY column_name DESC;`

We can even sort on multiple columns. 

EX:

`SELECT * FROM table_name ORDER BY column_name1 ASC, column_name2 DESC;`

What this does is, it sorts the data first by column_name1 and then, if any values of column_name1 are same, we would look at column_name2.


### Aggregates... The soul of SQL

Now, to the most important thing and also, the easiest. 
Aggregates are functions that take in multiple rows of input and give a single output or a statistic or some sort of metric. These functions answers questions like, "What is the average pay?", "How many employees are here?" et cetera. 
Think of it this way, ANYTHING THAT YOU CAN THINK OF THAT TAKES MULTIPLE ROWS AND GIVES A DESIRED OUTPUT IS PROBABLY AN AGGREGATE. It's as simple as that. 


Here are a few of the most important aggregates:

|Function|Description|Example|Result|
|---|---|---|---|
|`COUNT()`|Number of rows|`COUNT(*)`|`354`|
|`SUM()`|Adds up numeric values|`SUM(salary)`|`₹15,200,000`|
|`AVG()`|Average value|`AVG(age)`|`37.4`|
|`MIN()`|Smallest value|`MIN(salary)`|`₹35,000`|
|`MAX()`|Largest value|`MAX(salary)`|`₹420,000`|

Here is an example code snippet that covers all the functions of aggregation:

```
SELECT 
COUNT(*) AS count,
SUM(salary) AS sum_of_all_salaries,
AVG(salary) AS avg_salary,
MIN(salary) AS min_salary,
MAX(salary) AS max_salary
FROM table_name;
```

*We named each value we derived as something and then we made a table out of it to present to the user. That is why we used AS. The column names are right beside the AS part.*

We didn't pass in salary for count() as well because count doesn't count NULL values. Say that a few employees have their salaries set to NULL for some reason. Then, we simply won't be able to get the real number of employees. However, if there is a select all type of operation, we will get the actual number of people in the table.

We can also filter the things we are operating on. Here is an example:

`SELECT MAX(salary) FROM table_name WHERE due IS NOT NULL;`

We are checking the max salary where there are no dues. That is how to use a filter with these functions. 

### GROUPS

Groups is just aggregation on steroids. To understand this topic to it's extreme, we first need to know why it's used. Look at this question:

`Write a query to find the highest salary in each department.`

In this particular question, we need to solve it by finding the highest salary in each department separately and then presenting it all together in a single table with each row being each department and each row containing the max salary of that particular department. So, we need to run aggregate n number of times where n is the number of departments. In order to do that, we use groups. Here is an example of how groups work:

```
SELECT dept_no, MAX(salary) AS max_salary
FROM salary_table
GROUP_BY dept_no;
```

What we are doing here is, we are creating a table that contains a dept_no and max_salary and we are grouping by dept_no. 

**THE MOST IMPORTANT THING TO NOTE HERE IS, EVERY COLUMN OTHER THAN THE COLUMN WE ARE GROUPING BY NEEDS TO BE UNDER AN AGGREGATING FUNCTION. IF YOU THINK ABOUT IT, THERE IS A LOGIC BEHIND IT. BUT IT'S A TOUGHER ONE TO GRASP. SO REMEMBERING THIS ONE THING WON'T HURT.***
also, NULL is also considered a group. Remember that.

We can also group by multiple columns. Here is an example.

```
SELECT dept_no, job_title, MAX(salary) AS max_salary
FROM salary_table
GROUP_BY dept_no, job_title;
```

What this does is, it creates a new row for every combination of dept_no and job_title. This is good for you.

Just as we use WHERE in aggregations, we use HAVING in groups. Here is a quick example on how:

```
SELECT dept_no, COUNT(*) AS count_per_dept
FROM table_name
HAVING COUNT(*) > 2;
```

The most important thing here is, "count_per_dept" is considered not as a variable but as a column name. We cannot use count_per_dept > 2 because that is not a variable yet. However, if we make the quiery a sub quiery, that is possible. This works.

```
SELECT * FROM
(SELECT dept_no, COUNT(*) AS count_per_dept
FROM table_name) AS t
HAVING count_per_dept > 2;
```


### SUBQUERIES AND NESTED QUERIES

Simply, A SELECT statement inside any other statement (SELECT, INSERT, DELETE, ET CETERA) is called a subquery. Now, multiple layers of queries are called nested subqueries. 

There are different types of subqueries:

- One that returns a scalar quantity (Scalar subquery (max, min, avg et cetera))
- One that returns a row (row subquery)
- One that returns a table (derived table)
- One that returns it's entire self (self-returning subquery used in IN ALL ANY et cetera)

There are also 2 types of subqueries based on the relationship between the main query and the subquery:

#### Correlated Subquery

Here, The subquery is interlinked with the main query and doesn't make proper sense without it. Here is an example:

```
SELECT e.name
FROM employees e
WHERE e.salary > (
  SELECT AVG(salary) FROM employees WHERE dept_id = e.dept_id
);
```

Here, clearly we are using the major queries variables inside the subquery.


#### Uncorrelated Subquery

Here, the subquery doesn't need the main query to make sense. It can be a stand alone block of code. Here is an example:

```
SELECT name FROM employees
WHERE dept_id = (SELECT id FROM departments WHERE name = 'Sales');
```

##### Membership Checks

In the context of subqueries and operators, here is a block of code you might be interested in:

```
SELECT c.*
FROM customers c
WHERE EXISTS (
  SELECT 1 FROM orders o WHERE o.customer_id = c.id
);
```

Here, we are checking if there is at least 1 row such that `o.customer_id` equals `c.id`. If there is, we will return True. Else, we will return False. So, this is a Boolean membership check situation. 



### UPDATE AND SET

These update and set commands are two different commands which work together to change a certain column's data. Here is an example:

```
UPDATE employee
SET col1 = x.col1,
col2 = x.col2,
col3 = x.col3
WHERE x.id > 0;
```

What this does is, it helps us update the values inside a table. The stuff we have learnt thus far didn't teach us how to update or change the data we have inside an already existing table and already existing values. This does exactly that. You chose the table you want the changes to occur in, you set each column to a desired column(usually self changed or another column from another table entirely) and you apply a condition on which you want the changes to happen. You have to be careful when you are setting a column to another column located somewhere else because it might have a different size or even a different datatype. Be mindful of all these situations in order to avoid fatal flaws in your code. 


### Normalization

This concept is pretty simple. Just like we have good practices in coding (good spacing, nice naming of variables et cetera), we have normalization in SQL. There are a few rules that, if we follow, would render our tables clean without any redundancies. We can each rule "normal form". Here is the table of general rules to follow :

|Normal Form|Goal|Key Rule|
|---|---|---|
|**1NF (First Normal Form)**|Remove repeating groups|Each column must contain atomic (indivisible) values, and each row must be unique|
|**2NF (Second Normal Form)**|Remove partial dependency|Table must be in 1NF and all non-key attributes fully depend on the **whole primary key**|
|**3NF (Third Normal Form)**|Remove transitive dependency|Table must be in 2NF and all non-key attributes depend **only on the primary key**, not other non-key columns|
|**BCNF (Boyce-Codd NF)**|Handle edge cases beyond 3NF|Every determinant must be a candidate key|
|Higher NFs (4NF, 5NF)|Handle multi-valued & join dependencies|Mostly used in complex databases|

If we bear these in mind while we make tables, our tables will be much cleaner. It all comes down to practice for this. There is nothing much to explain here.

Here is the most fundamental thing you should always be aware of. If your table has multiple many to many relationships, that is a bad table. You need to maintain it such that each table has at the most 1 many-to-many relationships.

---
This single problem will teach us different, highly essential, concepts of SQL

`Write a query to find all employees who have been with the company for more than 5 years.`

In order to solve this problem, we first have to find a way to check the age of the employee according to the company. That requires the current date and the date of their joining. The solution goes like this with the help of the following functions:

- CURDATE(): This returns the current date (16-10-2025) in DD-MM-YYYY format.
- TIMESTAMPDIFF(unit, start_date, end_date) : This function is the gold standard to find the difference between dates. unit = year or month or day. Whatever unit you give, it returns the difference in that unit. Say I want my 1 and 3 days employee's work span in months. It will return 12. suppose I want it in days, it will return 368. 
- DESCRIBE keyword: This keyword helps us see the type of object our columns are storing, be it int or VARCHAR or anything. How to use this??
  `DESCRIBE table_name`
  and this gives a comprehensive table describing the different metadata of that table. 

Now, combining all this together, we can solve the problem like so:
```
SELECT * FROM table_name WHERE TIMESTAMPDIFF(DAY, from_date_column, CURDATE()) > (5*365)
```

We calculated in days because I felt like that was more accurate. It all boils down to you.

---


### Transactions

This concept is fairly simple. Sometimes, we want a bunch of code to run together and if some of it fails, we want to stop the entire process. That is where we use transactions. It's major use is in banking and money related situations because say that an append works but deduction doesn't work, then we just created money out of thin air. That is a huge problem. That is why transactions exist. Here is how you implement them:

```
START TRANSACTION;

-- doing some changes
UPDATE employee SET pay = pay + 10000 WHERE industry = 'IT';

UPDATE employee SET pay = pay - 10000 WHERE industry = 'Finance';

-- We are commiting if both of the lines work
COMMIT;

-- Or we will not do anything
ROLLBACK;
```

So essentially, we are doing both of these tasks or none of them. They need to be done together or all goes to hell. That is when a transaction is useful.

Now, the most fundamental part of a transaction is security and sanctity. So it is natural for this question to form : `How would you handle errors during a transaction to ensure data integrity?`

to solve this particular problem, there are a LOT of different things we can do. I will list some of them here:

SAVEPOINTS:

 - This concept allows users to save progress to a certain extent when we want in a transaction. Now, take this code to understand how save points work:

  ```
	START TRANSACTION;
		-- step A
		SAVEPOINT sp_a;
		-- step B (might fail)
		SAVEPOINT sp_b;
		-- something fails:
		ROLLBACK TO SAVEPOINT sp_b;   -- undo only after sp_b
		-- continue or finally
	COMMIT;

  ```


Say in a situation, for some reason, you need to save the progress up to a certain point. Use the `SAVEPOINT name_of_save_point` code. What we are doing here is essentially telling the commit if the next steps pass, we also take them in. But if they fail, which they might, we only take what's up to the save point. 

- `InnoDB` engine needs to be used in order to use any of these (transactions, save points et cetera)

- DEADLOCKS
	 A dead lock is a situation where two queries are locked together and cannot move. Example would be, say a transaction is needs to access row 1 and 2. Say another transaction also needs to do that. what happens is, they are at a standoff neither willing to wait. This leads to indefinite hangs and straight up crashes. To prevent this, we have methods. Here is the detailed explanation of the whole thing from AI:
	 **What is a deadlock?**
		Imagine **two or more transactions** trying to access the same data in a database **at the same time**.   
		If Transaction A holds a lock on Row 1 and waits for Row 2, while Transaction B holds a lock on Row 2 and waits for Row 1 → **neither can proceed**.
		This situation is called a **deadlock**.
> 		Analogy: Two people blocking each other in a narrow hallway, each waiting for the other to move.
> 		
    Why it matters
	 Deadlocks prevent transactions from completing.
	 If unhandled, your application may **hang indefinitely** or throw errors.
	1. Catch deadlock errors (MySQL error codes like `1213)
	MySQL **detects deadlocks automatically** and will abort **one of the conflicting transactions** to resolve the deadlock.    
	It reports the error with **code 1213** (`ER_LOCK_DEADLOCK`) and a message like “Deadlock found when trying to get lock; try restarting transaction.”
	“Catch” means: in your **application code**, detect this error and **handle it gracefully**, instead of letting it crash the app.
	`try:     cursor.execute("some transactional SQL") except mysql.connector.Error as err:     if err.errno == 1213:  # deadlock error         # handle retry here`
	Retry the whole transaction with exponential backoff:
	Retry the whole transaction: After a deadlock, you usually **re-run the entire transaction** from scratch, because it was aborted.
	Exponential backoff: Wait a bit before retrying, and increase the wait time each time.
	 Example: wait 100ms → 200ms → 400ms …
	Prevents **multiple transactions from colliding repeatedly**, reducing load and contention.
			
4. Make retries idempotent
		
	What is idempotency?
		A process is **idempotent** if **running it multiple times has the same effect as running it once**.   
		- This is crucial because **retrying a transaction after deadlock** might run **some queries twice** if not handled carefully.		
		**Example:**
		- Bad:
		    `INSERT INTO orders (id, user_id) VALUES (NULL, 1);`
		    - Retrying can insert **duplicate rows**    
		- Good (idempotent / with idempotency key):
		    `INSERT INTO orders (idempotency_key, user_id) VALUES ('abc123', 1) ON DUPLICATE KEY UPDATE ...;`
		    - Retrying does **not create duplicates**, transaction can safely be re-run.

### Difference between Delete and `Turncate`

Delete:

This is a keyword used when you want to delete rows row-by-row. This also allows conditional functionality. But the core drawback is, it takes a lot of time on large databases because it does it's operations row-by-row. Useful when we want to selectively delete stuff or remove a small table. 

`DELETE TABLE table_name WHERE condition_if_need_be;`


Turncate:

This is a keyword used when you want to delete an entire table. No conditions are allowed. This completely erases the table from existence and in some versions of SQL, this cannot be rolled back. So use this carefully. This takes far less time than delete though, because it directly deallocates the memory the table holds, rendering it useless.  

`TURNCATE TABLE table_name;`


### KEYS

There are two different types of keys. 

- Foreign Key
- Primary Key

These two are inter-related. A foreign key is a column (or a group of columns) in one table that reference to the primary key of another table. This creates a link between two given tables. 
Here is an example code snippet:

```
CREATE TABLE Departments (
    dept_id INT PRIMARY KEY,
    dept_name VARCHAR(50)
);

CREATE TABLE Employees (
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(50),
    dept_id INT,
    FOREIGN KEY (dept_id) REFERENCES Departments(dept_id)
);

```

What we did here is, we are linking table departments and employees via the `dept_id` column. This sort of establishes relational integrity between tables. How is that done? there are certain rules that these references follow that ensure top notch integrity.

- INSERT RULE: 
	You cannot insert a row in the foreign key column if it does not exist in the primary key column. This means that the foreign key column will always be a subset to the primary one.
- UPDATE RULE:
    You cannot update a row such that the link between the primary and the foreign keys are broken. You must use something called a `cascade` which we will talk about soon.
- DELETE RULE:
	You cannot delete a row in the parent table if it is still referenced in the child table. It is pretty clear that the primary key is the parent table and the foreign key table is the child table. Of course you can use the same `cascade` keyword to delete rows, which we will talk about soon.

Following these rules maintain a well maintained relationship between tables without having 'orphan' rows or records.

**CASCADE** :

what cascade does is, it allows the deletion of parent rows without any errors or trouble. During the usage of a cascaded foreign key, when a parent is deleted, all of it's children are deleted. This maybe a desired quality sometimes but not desirable other times. So better be careful when you write that CASCADE line. Here is the syntax for it:

```
CREATE TABLE employee(
emp_id INT PRIMARY KEY,
pay INT,
);

CREATE TABLE tech(
emp_id INT,
FOREIGN KEY (emp_id) REFERENCES employee(emp_id)
ON DELETE CASCADE
ON UPDATE CASCADE
);
```

What we did here is, we set cascade on delete and update operations. What this does is, once a parent is deleted or updated, the effects are passed down it's children. There can be any number of generations of keys. 

### CONSTRAINTS

I know this concept should have been further up of this note, but hey, it is here:

Constraints are something we use during the initialization of a column. Along side the name, datatype of the column, we also decide the constraints of the column. 

Here are a few constraints to know:

|Constraint|What it does|Example|
|---|---|---|
|**PRIMARY KEY**|Uniquely identifies each row in a table|`emp_id INT PRIMARY KEY`|
|**FOREIGN KEY**|Ensures a column’s value exists in another table|`FOREIGN KEY (dept_id) REFERENCES Departments(dept_id)`|
|**UNIQUE**|Ensures all values in a column are unique|`email VARCHAR(50) UNIQUE`|
|**NOT NULL**|Ensures a column cannot have NULL values|`name VARCHAR(50) NOT NULL`|
|**CHECK**|Ensures a condition is true for values in a column|`age INT CHECK (age >= 18)`|
|**DEFAULT**|Provides a default value if none is given|`status VARCHAR(10) DEFAULT 'active'`|

Here is the syntax for all of these: (We will be excluding keys here cuz they were already written above)

UNIQUE:

```
CREATE TABLE name_of_table(
a INT UNIQUE,
b INT UNIQUE,
c INT
);
```


What this does is, it only takes unique a and unique b but any c. We cannot have the same no matter the b and c values, similarly, we cannot have same b values no matter what the a, c values are. 

But we can also write like this

```
CREATE TABLE name_of_table(
a INT,
b INT,
c INT,
UNIQUE(a,b,c)
);
```

What this does is, it only takes in unique (a, b, c) pairs. if we set unique only to (a, b) it makes sure that (a, b) is unique and doesn't care about c at all. You will get this with practice.

NOT NULL:

```
CREATE TABLE name_of_table(
a INT NOT NULL
);
```

What that means is, it doesn't take a row if a is NULL. Pretty straight forward.

CHECK:

```
CREATE TABLE name_of_table(
a INT CHECK (a < 10)
);
```

It only takes in values of a if they are less that 10.

DEFAULT:

```
CREATE TABLE name_of_table(
a INT DEFAULT 10
);
```

What this does is, if no value is given, it gives a default value of 10.

Note that any of these can be written at the end too, like this

```
CREATE TABLE name_of_table(
a INT,
DEFAULT(a) 10
);
```

This and that are both the same. This works for every constraint here.


### SLOW-QUERIES

Identifying slow queries is one of the most important things you should learn when you are trying to optimizing queries. Finding the worst performers is one of the most important things you can do. Now, there are several steps we can take to find out the slow queries. 

- ##### SLOW QUERY LOGS
	Here is the syntax to understand how this goes:
	```
	
	-- first thing we are going to do is, activate slow query logging
	SET GLOBAL slow_query_log = 'ON';
	--- we tell where the log must be logged. 
	SET GLOBAL slow_query_log_file = '/var/log/mysql/slow.log';
	-- We tell the computer that if the log takes more than 1 second,to log it.
	SET GLOBAL long_query_time = 1;
		
	```
This helps us see the logs at this address '/var/log/mysql/slow.log'. All these logs are of bad queries.

- #### EXPLAIN
    'Explain' is a keyword used to explain tables. Here is how it works.
    `EXPLAIN SELECT * FROM table_name WHERE condition;`
	We will get all the metadata from that query including the time it took for the query to run.

- #### PERFORMANCE SCHEMA
  MySQL has a performance schema table that has all the performance details we can ever ask for. The way you access it is like this:
  ```
  SELECT performance_schema.events_statements_summary_by_digest ORDER BY AVG_TIME_WAIT DESC; 
  ```
What this gives you is a table of the time it took for each query ordered in the descending order.
This is not of much help tho. So be careful when using this.


### INDEXING

In SQL, you can index each column. You don't need to index a table by it's rows like a normal table. We can index each column and here is how you do it:

```
CREATE INDEX index_name ON orders(name_of_the_column);
```

These indexes can also be composite:

```
CREATE INDEX inde_name ON orders(col_name1, col_name2, et cetera...);
```

What this does is, it creates the same indices for all the columns mentioned above. If you give all the columns in the table, you are asking for a whole tabular index. Simple.

These allow us to quickly read files because it helps SELECT a lot to have columns indexed. However, it is computationally heavy to write indices for every single column. Therefore, when a particular column is read heavy, we use indices for that column. When a particular column is write heavy, you tend not to use indices there. Try to use `performance_schema` to see which indices are becoming a problem to your commands. Note that InnoDB (the engine of MySQL we all tend to use) is highly optimized for write. So, this allows us to use indices more often but it doesn't mean we should use them everywhere.


### PROCEDURE & FUNCTIONS

A procedure stores code and runs it on command. The syntax goes like this:

```
DELIMITER $$

CREATE PROCEDURE name_of_the_procedure(
IN variable_name1 data_type,
IN variable_name2 data_type,
IN variable_name3 data_type,
....
....
....
)
BEGIN
	--the commands we need to run should be written here
END $$

DELIMITER ;	

CALL name_of_the_procedure(var1, var2, var3 ...);
```

This is the general layout of the procedure. Now, let's explain each step.

- `DELIMITER $$/ DELIMITER`
	Each procedure is wrapped in `DELIMITER $$/DELIMITER` because we want to delimit the number of commands we can run inside the function. This allows us to use multi-statement procedures. Note that the DELIMITER ending the whole thing has to have a space between it and the semi-colon or you get an error.
- IN
	The keyword `IN` is used to represent input variables. We then explain the name of the variable to the computer and then the datatype. This is just like creating a table. 
- `BEGIN/END $$`
	These represent the start and end of the procedure.
- `CALL`
	The call is written to use the procedure whenever we want. you just give it the variables and it does what it needs to. 

Here is an example procedure and it's call:

```
USE employee;

DELIMITER $$
CREATE PROCEDURE insert_name(
IN emp_no_in INT,
IN amount_in INT,
IN from_date_in DATE,
IN to_date_in DATE
)
BEGIN
INSERT INTO salary(emp_no, amount, from_date, to_date) VALUES(emp_no_in, amount_in, from_date_in, to_date_in);
END $$
DELIMITER ;

CALL insert_name(1111, 9999999, '2028-06-06', '2028-07-07');

```

There is one more thing to bear in mind here. Once a procedure is read by the workbench, it stores this procedure. That means, when you run the code again with this being in the code, you will run into an error saying that the procedure named `name_of_the_procedure` already exists. Just comment out the procedure.

We call these procedures and not functions for a reason. In MySQL, functions are a different sort of breed. 

There are a few fundamental differences between a procedure and a function:

| Aspect                   | Stored Procedure                                                                                       | Function                                                                                         |
| ------------------------ | ------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------ |
| **Purpose**              | Performs actions (insert, update, delete, complex logic). Can return multiple result sets or no value. | Computes and **returns a single value**. Usually used in expressions.                            |
| **Return Type**          | Optional (`OUT` parameters), can return 0 or more values via parameters.                               | **Mandatory** `RETURN <value>` of a specific type.                                               |
| **Usage in SQL**         | Invoked via `CALL procedure_name(...)`. Cannot be used inside a SQL expression.                        | Can be used in SQL queries, e.g., `SELECT func_name(...)`.                                       |
| **Side Effects**         | Can modify data (INSERT, UPDATE, DELETE).                                                              | Generally should not have side effects. MySQL allows modification, but it’s **not recommended**. |
| **Transaction Handling** | Can include multiple statements, loops, and conditional logic.                                         | Simpler, usually one expression or computation.                                                  |
| **Error Handling**       | Can use `DECLARE ... HANDLER`.                                                                         | Limited error handling; mostly relies on returning a valid value.                                |

So basically, you use a function when you need something returned (like when we are using a conditional statement) and the computation inside that said function is light (1-2 commands). Other-wise, procedures are prefered. Here is how you write a function:

```
DELIMITER $$

CREATE FUNCTION is_active(emp_no_in INT)
RETURNS BOOLEAN
DETERMINISTIC
READS SQL DATA
BEGIN
    DECLARE result BOOLEAN;
    
    SELECT CASE WHEN status = 'active' THEN TRUE ELSE FALSE END
    INTO result
    FROM employee
    WHERE emp_no = emp_no_in;
    
    RETURN result;
END $$

DELIMITER ;

```

You will notice a few odd things here.
- First of all, let's talk about the lack of `IN` while we are passing parameters into the function. That is because, all input variables are IN for a function but for a procedure, you have to explicitly tell the PC what it is. Here is how IN OUT INOUT works:

```
DELIMITER $$

CREATE PROCEDURE demo_proc(
    IN in_val INT,
    OUT out_val INT,
    INOUT inout_val INT
)
BEGIN
    SET out_val = in_val * 2;        -- returning new value via OUT
    SET inout_val = inout_val + 10;  -- modifying INOUT value
END $$

DELIMITER ;

SET @a = 5, @b = 0, @c = 7;
CALL demo_proc(@a, @b, @c);
SELECT @b, @c;  -- @b = 10 (OUT), @c = 17 (INOUT)

```

What you are seeing here is the usage of IN OUT INOUT keywords. IN means INPUT. OUTPUT means OUPUT. INOUT is both input and output. So it will be output no matter what. So once the CALL ends, what the workbench does is, it sends back the OUT AND INOUT variables to the computer successfully updating the variables that are declared outside the procedure. Why we don't have this in functions is because there is a RETURN statement we can use in functions unlike PROCEDUREs. 

- The next thing we would notice is the declaration of `RETURNS BOOLEAN`. We are disclosing the return type of the function early.
- The next confusion we get is from the `DETERMINISTIC/NON-DETERMINISTIC` keywords. Deterministic means, if the same inputs are given, do we always get the same output? if 1 is given as input, if sometimes we get 2 and sometimes we get 10 as results, it's NON-DETERMINISTIC for sure. That's the simple rule of thumb. Here are examples of where you use that and this:

NON DETERMINISTIC

```
CREATE FUNCTION rand_int()
RETURNS INT
NOT DETERMINISTIC
BEGIN 
RETURN FLOOR(1 + (RAND()* 100));
END $$
```

DETERMINISTIC

```
CREATE FUNCTION calculate(
a_in INT,
b_in INT
)
RETURNS BOOLEAN
DETERMINISTIC
BEGIN
RETURN a_in = b_in; -- we use single equal for comparision in SQL
END $$
```

Note that it really doesn't crash your code if you are wrong about weather a function is deterministic or not. We write this purely for optimization's sake.

- The next line will tell the computer what sort of SQL commands we are using in the function. AGAIN, THIS IS NOT NEEDED FOR THE FUNCTIONING OF OUR FUNCTION, IT JUST ADDS EFFICIENCY TO OUR FUNCTION. Here are the different lines you can write there:

|Clause|Meaning|When to use|
|---|---|---|
|**NO SQL**|The function does **not contain any SQL statements**.|Pure computation like `RETURN a_in + b_in;`|
|**CONTAINS SQL**|The function **may contain SQL statements** but **does not modify data**.|Simple `SELECT` queries that don’t change tables.|
|**READS SQL DATA**|The function **reads from tables** but does **not modify data**.|`SELECT * FROM employee WHERE emp_no = a_in;`|
|**MODIFIES SQL DATA**|The function **modifies data** in the database (`INSERT`, `UPDATE`, `DELETE`).|Rare in functions; usually done in procedures instead.|


That's all there is to explain here.

- Next we see the code trying to create a boolean variable called result. It is done so like this `DECLARE var_name BOOLEAN`
- This is just a standard SQL line:

```
SELECT CASE WHEN status = 'active' THEN TRUE ELSE FALSE END
INTO result
FROM employee
WHERE emp_no = emp_no_in;
```

We are checking if the status is active. If it is, we are assigning true to result else false for a given employee number `emp_no_in`.


So this is how a function is written.

ERROR HANDLING:

In procedures, we error handle with the help of handler. Here is the blueprint of how it goes:

```
DECLARE handler_type HANDLER FOR condition_value
BEGIN
    -- handler logic
END;
```

`handler_type` is of two types. It's either continue or exit. what these do is tell the computer to either exit when the error is found or continue in spite of the error.

There could be a lot of `condition_values`. Here are a few:

| Condition         | Meaning                             |
| ----------------- | ----------------------------------- |
| `SQLEXCEPTION`    | Any error occurs                    |
| `SQLWARNING`      | A warning occurs                    |
| `NOT FOUND`       | e.g., `SELECT INTO` returns no rows |
| `SQLSTATE 'xxxx'` | Specific error code                 |


Here is an example to drive home the handling of errors:


```
DELIMITER $$

CREATE PROCEDURE divide_numbers(IN a INT, IN b INT, OUT result DECIMAL(10,2))
BEGIN
    DECLARE CONTINUE HANDLER FOR SQLEXCEPTION
    BEGIN
        SET result = NULL;  -- return NULL if any error occurs
    END;

    SET result = a / b;  -- will raise error if b = 0
END $$

DELIMITER ;

```


### TRIGGER

Triggers are these function like statements you give to the computer to do a certain action automatically when a certain trigger is 'pressed'. This comes in handy in a lot of places including, but not limited to, validation of data before entering to the database, setting caps to the data we enter, can create cascading updates, automatic audits etc. Now, here is the general layout of a TRIGGER:

```
CREATE TRIGGER trigger_name
{BEFORE | AFTER}{INSERT | DELETE | UPDATE}
ON table_name
FOR EACH ROW 
BEGIN
-- LOGIC HERE
END;
```

What we are essentially doing here is, for a given table, `table_name`, weather it is before a certain action (insert, delete, update) or after, do this action for each row.

Here is an example code to really drive it in:

```
CREATE TRIGGER salary_check
BEFORE INSERT 
ON salary_table
FOR EACH ROW
BEGIN
	IF NEW.amount < 10000 THEN
		SIGNAL SQLSTATE '45000'
		SET MESSAGE_TEXT = 'You cannot have salary less than 10k';
	END IF;
END; 
```

What this does is, before we are inserting into `salary_table`, we are telling the computer to run this code. That code checks if the amount is less than 10k. if it is, we are giving an error and setting the error message to some text. 


