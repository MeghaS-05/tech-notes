**PostgreSQL** is a free, open-source, object-relational database management system (ORDBMS) used to store, manage, retrieve, and manipulate data.

- It uses SQL (Structured Query Language).
- It supports relational tables and complex data types.
- It provides ACID-compliant transactions.
- It supports indexing, constraints, joins, and relationships.
- It supports JSON, arrays, custom data types, and extensions.
- It works with languages like Python, Java, JavaScript, PHP, and Go

PostgrSQL originated from a research project at the University of California, Berkeley.

Traditional relational databases had limitations when handling complex data and relationships. POSTGRES was developed to overcome these limitations.

**Main objectives:**

1. Support complex data types.
2. Support user-defined data types.
3. Handle complex relationships between data.
4. Provide extensibility.
5. Improve database functionality beyond traditional relational models.

### **Why is PostgreSQL popular?**

- **Open source:** Free to use and modify.
- **Reliability:** Supports ACID transactions.
- **Data integrity:** Supports primary keys, foreign keys, unique constraints, etc.
- **Performance:** Provides indexing and query optimization.
- **Extensibility:** Supports custom functions, data types, and extensions.
- **Scalability:** Supports large databases and concurrent users.
- **Compatibility:** Integrates with multiple programming languages.

### **PostgreSQL Architecture**

PostgreSQL follows a Client-Server Architecture. 

!image.png

**Working flow:**

1. Client sends an SQL query.
2. PostgreSQL receives the request.
3. Query is parsed and validated.
4. Query planner selects an execution plan.
5. Executor executes the query.
6. Results are returned to the client.

### **PostgreSQL Internal Component:**

#### **A. Postmaster (Main Server Process)**

- Main PostgreSQL server process.
- Starts and manages the database server.
- Accepts client connection requests.
- Creates backend processes for client connections.
- Monitors background processes.

#### **B. Backend Process**

- Each client connection generally gets its own backend process.
- Executes SQL queries.
- Communicates with shared memory.
- Returns query results to clients.

#### **C. Backend Process**

- **Checkpointer :** Manages checkpoint operations
- **Background Writer :** Writes dirty buffers to disk (A **dirty buffer** is a temporary spot in your computer's fast memory holding recent changes that haven't been permanently saved yet.)
- **WAL (Write-Ahead Log) Writer :** Writes WAL records to disk

(**a background database worker (most notably in PostgreSQL) that writes recorded changes from memory into a Write-Ahead Log (WAL) file on disk before those changes are applied to the main database files**.)

- **Autovaccum Launcher :** Starts automatic vaccum workers

 (automatic background process in PostgreSQL that cleans up deleted or outdated rows ("dead tuples") so the database can reuse that space and keep queries running fast.)

- **Archiver :** Archives completed WAL segments when enabled.

Below one is for archiver pointer :—|

- **WAL writer:** Writes recent database changes into the active WAL files on the main disk.
- **Archiver:** Takes those finished WAL files and copies them somewhere safe (`archive_command`) so you have a complete history of changes.

**Why It Matters**

- **Point-in-Time Recovery (PITR):** If someone accidentally deletes an entire table at 2:00 PM, you can restore an older base backup and replay the archived WAL files right up to 1:59 PM.
- **Standby / Replica sync:** Backup servers can read archived WAL files to stay caught up with the main database.

### **Query Processing Pipeline**

When you Execute :  “ SELECT * FROM WHERE age > 18; ” 

Postgresql processes it through these stages:

**Step 1 : Parser —** Checks SQL syntax, creates a parse tree, identifies SQL commands and expressions. 

**Step 2 : Analyzer —** Checks whether tables and columns exist, Checks data types, Checks permissions.

**Step 3 : Rewriter —** Applies query rewrite rules, expands views where applicable, modifies the query representation when required.

**Step 4 : Query Planner/ Optimizer —** Generates possible execution plans, Estimate their costs, Selects a suitable execution plan (Sequential Scan, Index Scan, Index Only Scan).

**Step 5 : Executor —** Executes the selected plan, Retrieves required data, performs filtering/sorting/joining etc, returns result. Overall the planner decides how to execute, the executor actually executes.

### **Shared Buffers**

Shared Buffer is a postgresql’s main shared emory area used for caching database pages. Instead of reading data from disk every time, Postgresql can reuse pages already present in memory.

Example : “ SELECT * FROM users WHERE id=10; ”

**Working:**

1. PostgreSQL checks whether the required page is in shared buffers.
2. If present, it can read the page from memory.
3. If absent, PostgreSQL reads it from disk into shared buffers.

**Benefits:**

- Reduces disk I/O.
- Improves query performance.
- Helps frequently accessed data remain cached.

### **WAL (Write Ahead Logging)**

A Mechanism Postgresql uses to maintain data durability and support crash recovery. 

Main principle : Changes must be recorded in WAL before the corresponding modified data pages are written to their permanent storage locations.

Working:

1. PostgreSQL modifies the relevant data in memory.
2. WAL records describing the changes are generated.
3. WAL records are flushed to durable storage when the transaction commits.
4. Modified data pages can be written to disk later.

**Why WAL is important:**

- Crash recovery.
- Transaction durability.
- Point-in-time recovery when properly configured.
- Streaming replication support.

Check WAL-related configuration:

```
SHOW wal_level;
SHOW archive_mode;
```

### **MVCC (Multi-Version Concurrency Control)**

Postgresql mechanism which allows multiple transaction to access data concurrently while maintaining data consistency. It allows multiple users to read and update the same data without unnecessarily blocking each other.

Main concept : Postgresql maintains multiple versions of rows instead of immediately overwriting id versions.  I**nstead of immediately replacing an old row when someone updates it, PostgreSQL creates a new version of that row.**

That's what we mean by *row versions*.

Example:

Initial table:

| **ID** | **Balance** |
| --- | --- |
| 1 | 1000 |

Transaction A:

```
BEGIN;

SELECT balance
FROM accounts
WHERE id = 1;
```

Transaction B:

```
UPDATE accounts
SET balance = 2000
WHERE id = 1;

COMMIT;
```

PostgreSQL maintains row versions so Transaction A can continue seeing data according to its transaction snapshot.

**Advantages:**

- Improves concurrent read/write operations.
- Readers generally don't block writers.
- Provides consistent snapshots.
- Supports transaction isolation.

**Disadvantage:** Old row versions can remain in the database, creating dead tuples.

This brings us to VACUUM.

### **VACUUM**

Postgresql maintenance operation that cleans up dead tuples(obsolete row versions) and makes their storage space reusable.

Suppose we have this table:

| **ID** | **Name** | **Age** |
| --- | --- | --- |
| 1 | Rahul | 25 |

Now execute:

```
UPDATE users
SET age = 26
WHERE id = 1;
```

PostgreSQL creates a new row version instead of immediately overwriting the old version.

Conceptually:

| **Row version** | **Age** | **Status** |
| --- | --- | --- |
| Old version | 25 | Dead tuple (eventually) |
| New version | 26 | Current tuple |

The old version cannot be removed while an active transaction might still need it.

Once it's no longer needed, it becomes eligible for cleanup.

**This is where VACUUM comes in.**

Without VACUUM, obsolete row versions can accumulate.

This can cause:

1. Increased disk space consumption.
2. Table bloat.
3. More unnecessary disk I/O.
4. Performance degradation in some workloads.
5. Transaction ID wraparound risk if freezing is neglected.

Therefore, VACUUM is important for PostgreSQL database health.

**Types of Vacuum**

A. **VACUUM** — Cleans up dead tuples and makes their space reusable. cmd : “ VACUUM users; ”

B. **VACUUM ANALYZE** — Perform vacuum and updates table statistics used by the query planner. cmd : “ VACUUM ANALYZE users; ”

C. **VACUUM FULL** — Rewrites the entire table to compact it and return unused space to the operating system. cmd : “ VACUUM FULL users; ”

D. **ANALYZE** — Updates statistical information used by the query planner. cmd : “ ANALYZE users; ”

Unlike VACUUM, it doesn’t clean dead tuples.

### **AUTOVACUUM**

**Autovacuum** is a background process in PostgreSQL that automatically performs VACUUM and ANALYZE operations to maintain database health.

**Why is it needed?**

- Cleans obsolete row versions (dead tuples).
- Prevents excessive table bloat.
- Updates statistics used by the query planner.
- Helps prevent transaction ID wraparound.

**How does it work?**

1. Monitors database tables.
2. Checks whether maintenance thresholds are reached.
3. Starts background workers.
4. Performs VACUUM and/or ANALYZE automatically.

**Important commands**

```
-- Check whether autovacuum is enabled
SHOW autovacuum;

-- Check dead tuple estimates
SELECT relname, n_dead_tup
FROM pg_stat_user_tables;

-- Check autovacuum settings
SHOW autovacuum_vacuum_threshold;
SHOW autovacuum_vacuum_scale_factor;
```

### **Installation & psql Commands**

**1. What is psql?**

**psql** is the command-line interface (CLI) used to interact with PostgreSQL databases.

Using psql, we can:

- Connect to databases.
- Execute SQL queries.
- Create and delete databases.
- Create tables.
- Manage users and permissions.
- Inspect database information.

**2. Connecting to PostgreSQL**

```
psql -U postgres
```

Here:

- **`psql`** → Starts PostgreSQL CLI.
- **`U`** → Specifies username.
- **`postgres`** → Default administrative user commonly created during installation.

Connect to a specific database:

```
psql -U postgres -d mydatabase
```

**3. Important psql commands**

Remember: psql commands starting with **`\`** are meta-commands, not SQL statements.

| **Command** | **Purpose** |
| --- | --- |
| **`\l`** | List all databases |
| **`\c dbname`** | Connect to a database |
| **`\dt`** | List tables |
| **`\d tablename`** | Describe a table |
| **`\du`** | List users and roles |
| **`\dn`** | List schemas |
| **`\di`** | List indexes |
| **`\dv`** | List views |
| **`\conninfo`** | Show connection information |
| **`\q`** | Exit psql |
| **`\h`** | SQL command help |
| **`\?`** | psql command help |

**4. Database creation commands**

Create a database:

```
CREATE DATABASE ecommerce;
```

Delete a database:

```
DROP DATABASE ecommerce;
```

Connect to the database:

```
\c ecommerce
```

**5. SQL command categories**

SQL commands are commonly grouped into five categories.

| **Category** | **Full form** | **Purpose** | **Identifies** |
| --- | --- | --- | --- |
| DDL | Data Definition Language | Defines database structures | If you’re creating, modifying or deleting database objects |
| DML | Data Manipulation Language | Inserts, updates and deletes data | If you’re inserting, updating or deleting records |
| DQL | Data Query Language | Retrieves data | If you’re fetching records |
| DCL | Data Control Language | Manages permissions | If you’re granting or removing database permissions |
| TCL | Transaction Control Language | Manages transactions | If you’re controlling a transaction |

Examples:

**DDL**

```
CREATE TABLE users (id INT);
ALTER TABLE users ADD COLUMN name VARCHAR(100);
DROP TABLE users;
```

**DML**

```
INSERT INTO users VALUES (1, 'Rahul');
UPDATE users SET name = 'Amit' WHERE id = 1;
DELETE FROM users WHERE id = 1;
```

**DQL**

```
SELECT * FROM users;
```

**DCL**

```
GRANT SELECT ON users TO app_user;
REVOKE SELECT ON users FROM app_user;
```

**TCL**

```
BEGIN;
COMMIT;
ROLLBACK;
SAVEPOINT sp1;
```

### SQL Commands

#### 1. Database commands (Basic)

| Command | Syntax | Example |
| --- | --- | --- |
| Create database | `CREATE DATABASE db_name;` | `CREATE DATABASE company;` |
| Show databases (psql) | `\l` | `\l` |
| Connect database (psql) | `\c db_name` | `\c company` |
| Drop database | `DROP DATABASE db_name;` | `DROP DATABASE company;` |
| Rename database | `ALTER DATABASE old RENAME TO new;` | `ALTER DATABASE company RENAME TO firm;` |
| Database size | `SELECT pg_size_pretty(pg_database_size('db_name'));` | `SELECT pg_size_pretty(pg_database_size('company'));` |

#### 2. Table commands (DDL)

| Command | Syntax | Example |
| --- | --- | --- |
| Create table | `CREATE TABLE table_name (...);` | `CREATE TABLE employees (id INT, name VARCHAR(50));` |
| Show tables (psql) | `\dt` | `\dt` |
| Describe table (psql) | `\d table_name` | `\d employees` |
| Add column | `ALTER TABLE table ADD COLUMN col datatype;` | `ALTER TABLE employees ADD COLUMN salary NUMERIC(10,2);` |
| Rename column | `ALTER TABLE table RENAME COLUMN old TO new;` | `ALTER TABLE employees RENAME COLUMN name TO full_name;` |
| Change datatype | `ALTER TABLE table ALTER COLUMN col TYPE datatype;` | `ALTER TABLE employees ALTER COLUMN salary TYPE NUMERIC(12,2);` |
| Drop column | `ALTER TABLE table DROP COLUMN col;` | `ALTER TABLE employees DROP COLUMN salary;` |
| Rename table | `ALTER TABLE old RENAME TO new;` | `ALTER TABLE employees RENAME TO staff;` |
| Drop table | `DROP TABLE table_name;` | `DROP TABLE employees;` |
| Empty table | `TRUNCATE TABLE table_name;` | `TRUNCATE TABLE employees;` |
| Create temporary table | `CREATE TEMP TABLE name (...);` | `CREATE TEMP TABLE temp_emp (id INT);` |

#### 3. Data manipulation commands (DML)

| Command | Syntax | Example |
| --- | --- | --- |
| Insert one row | `INSERT INTO table VALUES (...);` | `INSERT INTO employees VALUES (1, 'Raj');` |
| Insert specific columns | `INSERT INTO table (col1,col2) VALUES (...);` | `INSERT INTO employees (id,name) VALUES (2,'Amit');` |
| Insert multiple rows | `INSERT INTO table VALUES (...), (...);` | `INSERT INTO employees VALUES (3,'Sam'), (4,'John');` |
| Insert from another table | `INSERT INTO table SELECT ...;` | `INSERT INTO backup_emp SELECT * FROM employees;` |
| Select all | `SELECT * FROM table;` | `SELECT * FROM employees;` |
| Select columns | `SELECT col1,col2 FROM table;` | `SELECT id,name FROM employees;` |
| Update records | `UPDATE table SET col=value WHERE condition;` | `UPDATE employees SET name='Rahul' WHERE id=1;` |
| Delete records | `DELETE FROM table WHERE condition;` | `DELETE FROM employees WHERE id=2;` |
| Delete all records | `DELETE FROM table;` | `DELETE FROM employees;` |
| Return affected rows | `... RETURNING *;` | `DELETE FROM employees WHERE id=3 RETURNING *;` |

#### 4. Filtering and sorting commands

| Command | Syntax | Example |
| --- | --- | --- |
| WHERE | `SELECT * FROM table WHERE condition;` | `SELECT * FROM employees WHERE id=1;` |
| AND | `WHERE condition AND condition` | `WHERE salary > 20000 AND id > 2;` |
| OR | `WHERE condition OR condition` | `WHERE id=1 OR id=2;` |
| NOT | `WHERE NOT condition` | `WHERE NOT id=1;` |
| BETWEEN | `WHERE col BETWEEN a AND b` | `WHERE salary BETWEEN 20000 AND 50000;` |
| IN | `WHERE col IN (values)` | `WHERE id IN (1,2,3);` |
| NOT IN | `WHERE col NOT IN (values)` | `WHERE id NOT IN (1,2);` |
| LIKE | `WHERE col LIKE pattern` | `WHERE name LIKE 'R%';` |
| ILIKE | `WHERE col ILIKE pattern` | `WHERE name ILIKE 'r%';` |
| IS NULL | `WHERE col IS NULL` | `WHERE salary IS NULL;` |
| IS NOT NULL | `WHERE col IS NOT NULL` | `WHERE salary IS NOT NULL;` |
| ORDER BY | `ORDER BY col ASC/DESC` | `SELECT * FROM employees ORDER BY salary DESC;` |
| LIMIT | `LIMIT n` | `SELECT * FROM employees LIMIT 5;` |
| OFFSET | `OFFSET n` | `SELECT * FROM employees OFFSET 5;` |
| DISTINCT | `SELECT DISTINCT col FROM table;` | `SELECT DISTINCT department FROM employees;` |
| FETCH | `FETCH FIRST n ROWS ONLY` | `SELECT * FROM employees FETCH FIRST 5 ROWS ONLY;` |

#### 5. Aggregate functions

| Function | Syntax | Example |
| --- | --- | --- |
| COUNT | `COUNT(*)` | `SELECT COUNT(*) FROM employees;` |
| SUM | `SUM(column)` | `SELECT SUM(salary) FROM employees;` |
| AVG | `AVG(column)` | `SELECT AVG(salary) FROM employees;` |
| MIN | `MIN(column)` | `SELECT MIN(salary) FROM employees;` |
| MAX | `MAX(column)` | `SELECT MAX(salary) FROM employees;` |
| GROUP BY | `GROUP BY column` | `SELECT department, COUNT(*) FROM employees GROUP BY department;` |
| HAVING | `HAVING condition` | `SELECT department, COUNT(*) FROM employees GROUP BY department HAVING COUNT(*) > 2;` |

#### 6. Joins (Important)

| Join | Syntax / Example |
| --- | --- |
| INNER JOIN | `SELECT * FROM emp e INNER JOIN dept d ON e.dept_id=d.id;` |
| LEFT JOIN | `SELECT * FROM emp e LEFT JOIN dept d ON e.dept_id=d.id;` |
| RIGHT JOIN | `SELECT * FROM emp e RIGHT JOIN dept d ON e.dept_id=d.id;` |
| FULL OUTER JOIN | `SELECT * FROM emp e FULL OUTER JOIN dept d ON e.dept_id=d.id;` |
| CROSS JOIN | `SELECT * FROM emp CROSS JOIN dept;` |
| SELF JOIN | `SELECT a.name,b.name FROM emp a JOIN emp b ON a.manager_id=b.id;` |
| NATURAL JOIN | `SELECT * FROM emp NATURAL JOIN dept;` |

#### 7. Constraints

| Constraint | Syntax / Example |
| --- | --- |
| PRIMARY KEY | `id INT PRIMARY KEY` |
| FOREIGN KEY | `dept_id INT REFERENCES departments(id)` |
| UNIQUE | `email VARCHAR(100) UNIQUE` |
| NOT NULL | `name VARCHAR(50) NOT NULL` |
| CHECK | `age INT CHECK(age >= 18)` |
| DEFAULT | `status VARCHAR(20) DEFAULT 'active'` |
| Add primary key | `ALTER TABLE employees ADD PRIMARY KEY(id);` |
| Add foreign key | `ALTER TABLE employees ADD CONSTRAINT fk_dept FOREIGN KEY(dept_id) REFERENCES departments(id);` |
| Drop constraint | `ALTER TABLE employees DROP CONSTRAINT fk_dept;` |

#### 8. Subqueries

| Type | Example |
| --- | --- |
| Single-row subquery | `SELECT * FROM employees WHERE salary > (SELECT AVG(salary) FROM employees);` |
| Multiple-row subquery | `SELECT * FROM employees WHERE dept_id IN (SELECT id FROM departments);` |
| EXISTS | `SELECT * FROM departments d WHERE EXISTS (SELECT 1 FROM employees e WHERE e.dept_id=d.id);` |
| NOT EXISTS | `SELECT * FROM departments d WHERE NOT EXISTS (SELECT 1 FROM employees e WHERE e.dept_id=d.id);` |
| ANY | `SELECT * FROM employees WHERE salary > ANY (SELECT salary FROM employees WHERE dept_id=2);` |
| ALL | `SELECT * FROM employees WHERE salary > ALL (SELECT salary FROM employees WHERE dept_id=2);` |
| Correlated subquery | `SELECT * FROM employees e WHERE salary > (SELECT AVG(salary) FROM employees WHERE dept_id=e.dept_id);` |

#### 9. String functions

| Function | Example |
| --- | --- |
| UPPER | `SELECT UPPER('postgresql');` |
| LOWER | `SELECT LOWER('POSTGRESQL');` |
| LENGTH | `SELECT LENGTH('PostgreSQL');` |
| CONCAT | `SELECT CONCAT('Post','greSQL');` |
| SUBSTRING | `SELECT SUBSTRING('PostgreSQL',1,4);` |
| REPLACE | `SELECT REPLACE('PostgreSQL','SQL','DB');` |
| TRIM | `SELECT TRIM(' Hello ');` |
| LEFT | `SELECT LEFT('PostgreSQL',4);` |
| RIGHT | `SELECT RIGHT('PostgreSQL',3);` |
| POSITION | `SELECT POSITION('SQL' IN 'PostgreSQL');` |
| SPLIT_PART | `SELECT SPLIT_PART('a,b,c',',',2);` |

#### 10. Date and time functions

| Function | Example |
| --- | --- |
| Current date | `SELECT CURRENT_DATE;` |
| Current time | `SELECT CURRENT_TIME;` |
| Current timestamp | `SELECT CURRENT_TIMESTAMP;` |
| Extract year | `SELECT EXTRACT(YEAR FROM CURRENT_DATE);` |
| Extract month | `SELECT EXTRACT(MONTH FROM CURRENT_DATE);` |
| Add interval | `SELECT CURRENT_DATE + INTERVAL '7 days';` |
| Subtract interval | `SELECT CURRENT_DATE - INTERVAL '1 month';` |
| Date difference | `SELECT DATE '2026-12-01' - DATE '2026-11-01';` |
| Date truncation | `SELECT DATE_TRUNC('month', CURRENT_DATE);` |
| Age | `SELECT AGE(DATE '2026-11-25', DATE '2000-01-01');` |
| Formatting | `SELECT TO_CHAR(CURRENT_DATE, 'DD-MM-YYYY');` |

#### 11. Conditional expressions

| Command | Example |
| --- | --- |
| CASE | `SELECT CASE WHEN salary > 50000 THEN 'High' ELSE 'Low' END FROM employees;` |
| COALESCE | `SELECT COALESCE(NULL, 100);` |
| NULLIF | `SELECT NULLIF(10,10);` |
| GREATEST | `SELECT GREATEST(10,20,30);` |
| LEAST | `SELECT LEAST(10,20,30);` |

#### 12. Set operations

| Operator | Example |
| --- | --- |
| UNION | `SELECT name FROM emp1 UNION SELECT name FROM emp2;` |
| UNION ALL | `SELECT name FROM emp1 UNION ALL SELECT name FROM emp2;` |
| INTERSECT | `SELECT name FROM emp1 INTERSECT SELECT name FROM emp2;` |
| EXCEPT | `SELECT name FROM emp1 EXCEPT SELECT name FROM emp2;` |

#### 13. Views

| Command | Example |
| --- | --- |
| Create view | `CREATE VIEW emp_view AS SELECT id,name FROM employees;` |
| Read view | `SELECT * FROM emp_view;` |
| Replace view | `CREATE OR REPLACE VIEW emp_view AS SELECT * FROM employees;` |
| Drop view | `DROP VIEW emp_view;` |
| Create materialized view | `CREATE MATERIALIZED VIEW emp_summary AS SELECT department,COUNT(*) FROM employees GROUP BY department;` |
| Refresh materialized view | `REFRESH MATERIALIZED VIEW emp_summary;` |
| Drop materialized view | `DROP MATERIALIZED VIEW emp_summary;` |

#### 14. Indexes

| Command | Example |
| --- | --- |
| Create index | `CREATE INDEX idx_name ON employees(name);` |
| Unique index | `CREATE UNIQUE INDEX idx_email ON employees(email);` |
| Composite index | `CREATE INDEX idx_dept_salary ON employees(dept_id,salary);` |
| Descending index | `CREATE INDEX idx_salary ON employees(salary DESC);` |
| Partial index | `CREATE INDEX idx_active ON employees(id) WHERE status='active';` |
| Expression index | `CREATE INDEX idx_lower_name ON employees(LOWER(name));` |
| Drop index | `DROP INDEX idx_name;` |
| Reindex | `REINDEX TABLE employees;` |

#### 15. Common Table Expressions (CTE)

| Command | Example |
| --- | --- |
| Basic CTE | `WITH temp AS (SELECT * FROM employees) SELECT * FROM temp;` |
| Multiple CTEs | `WITH a AS (SELECT * FROM employees), b AS (SELECT * FROM departments) SELECT * FROM a,b;` |
| Recursive CTE | `WITH RECURSIVE nums AS (SELECT 1 AS n UNION ALL SELECT n+1 FROM nums WHERE n<5) SELECT * FROM nums;` |
| CTE with UPDATE | `WITH updated AS (UPDATE employees SET salary=50000 WHERE id=1 RETURNING *) SELECT * FROM updated;` |

#### 16. Window functions (Advanced)

| Function | Example |
| --- | --- |
| ROW_NUMBER | `SELECT name, ROW_NUMBER() OVER(ORDER BY salary DESC) FROM employees;` |
| RANK | `SELECT name, RANK() OVER(ORDER BY salary DESC) FROM employees;` |
| DENSE_RANK | `SELECT name, DENSE_RANK() OVER(ORDER BY salary DESC) FROM employees;` |
| NTILE | `SELECT name, NTILE(4) OVER(ORDER BY salary) FROM employees;` |
| LAG | `SELECT salary, LAG(salary) OVER(ORDER BY id) FROM employees;` |
| LEAD | `SELECT salary, LEAD(salary) OVER(ORDER BY id) FROM employees;` |
| FIRST_VALUE | `SELECT FIRST_VALUE(salary) OVER(ORDER BY salary DESC) FROM employees;` |
| LAST_VALUE | `SELECT LAST_VALUE(salary) OVER(ORDER BY salary ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING) FROM employees;` |
| Running total | `SELECT salary, SUM(salary) OVER(ORDER BY id) FROM employees;` |
| Partition | `SELECT department, salary, AVG(salary) OVER(PARTITION BY department) FROM employees;` |

#### 17. Transactions (TCL)

| Command | Example |
| --- | --- |
| BEGIN | `BEGIN;` |
| COMMIT | `COMMIT;` |
| ROLLBACK | `ROLLBACK;` |
| SAVEPOINT | `SAVEPOINT sp1;` |
| Rollback to savepoint | `ROLLBACK TO SAVEPOINT sp1;` |
| Release savepoint | `RELEASE SAVEPOINT sp1;` |
| Set isolation | `SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;` |

#### 18. Stored procedures and functions

| Command | Example |
| --- | --- |
| Create function | `CREATE FUNCTION add_num(a INT,b INT) RETURNS INT LANGUAGE SQL AS 'SELECT a+b';` |
| Execute function | `SELECT add_num(10,20);` |
| Create procedure | `CREATE PROCEDURE update_salary() LANGUAGE SQL AS 'UPDATE employees SET salary=50000 WHERE id=1';` |
| Call procedure | `CALL update_salary();` |
| Drop function | `DROP FUNCTION add_num(INT,INT);` |
| Drop procedure | `DROP PROCEDURE update_salary();` |

#### 19. Triggers

| Command | Example |
| --- | --- |
| Create trigger function | `CREATE FUNCTION log_changes() RETURNS TRIGGER LANGUAGE plpgsql AS $$ BEGIN RETURN NEW; END; $$;` |
| Create trigger | `CREATE TRIGGER emp_trigger BEFORE UPDATE ON employees FOR EACH ROW EXECUTE FUNCTION log_changes();` |
| Drop trigger | `DROP TRIGGER emp_trigger ON employees;` |
| Disable trigger | `ALTER TABLE employees DISABLE TRIGGER emp_trigger;` |
| Enable trigger | `ALTER TABLE employees ENABLE TRIGGER emp_trigger;` |

#### 20. JSON and JSONB commands

| Command | Example |
| --- | --- |
| Create JSON column | `CREATE TABLE products(data JSONB);` |
| Insert JSON | `INSERT INTO products VALUES ('{"name":"Laptop","price":50000}');` |
| Get JSON value | `SELECT data->'name' FROM products;` |
| Get text value | `SELECT data->>'name' FROM products;` |
| Check key exists | `SELECT * FROM products WHERE data ? 'name';` |
| Containment | `SELECT * FROM products WHERE data @> '{"name":"Laptop"}';` |
| Update JSON | `UPDATE products SET data=jsonb_set(data,'{price}','60000') WHERE data->>'name'='Laptop';` |
| JSON keys | `SELECT jsonb_object_keys(data) FROM products;` |

#### 21. Advanced PostgreSQL commands

| Feature | Syntax / Example |
| --- | --- |
| UPSERT | `INSERT INTO employees(id,name) VALUES(1,'Raj') ON CONFLICT(id) DO UPDATE SET name=EXCLUDED.name;` |
| Conflict ignore | `INSERT INTO employees(id,name) VALUES(1,'Raj') ON CONFLICT(id) DO NOTHING;` |
| RETURNING | `INSERT INTO employees(id,name) VALUES(5,'Sam') RETURNING *;` |
| DISTINCT ON | `SELECT DISTINCT ON(dept_id) * FROM employees ORDER BY dept_id,salary DESC;` |
| FILTER | `SELECT COUNT(*) FILTER (WHERE salary>50000) FROM employees;` |
| LATERAL JOIN | `SELECT * FROM departments d CROSS JOIN LATERAL (SELECT * FROM employees e WHERE e.dept_id=d.id LIMIT 2) x;` |
| Generate series | `SELECT generate_series(1,10);` |
| Advisory lock | `SELECT pg_advisory_lock(123);` |
| Release lock | `SELECT pg_advisory_unlock(123);` |
| Explain query | `EXPLAIN SELECT * FROM employees;` |
| Analyze query | `EXPLAIN ANALYZE SELECT * FROM employees;` |

#### 22. User, role and permission commands (DCL)

| Command | Example |
| --- | --- |
| Create user | `CREATE USER raj WITH PASSWORD 'pass123';` |
| Create role | `CREATE ROLE developer;` |
| Grant permission | `GRANT SELECT ON employees TO developer;` |
| Grant all permissions | `GRANT ALL PRIVILEGES ON employees TO developer;` |
| Revoke permission | `REVOKE INSERT ON employees FROM developer;` |
| Add role membership | `GRANT developer TO raj;` |
| Remove role membership | `REVOKE developer FROM raj;` |
| Change password | `ALTER USER raj WITH PASSWORD 'newpass';` |
| Drop user | `DROP USER raj;` |
| List users (psql) | `\du` |

#### 23. PostgreSQL system and maintenance commands

| Command | Example |
| --- | --- |
| Show version | `SELECT VERSION();` |
| Current database | `SELECT CURRENT_DATABASE();` |
| Current user | `SELECT CURRENT_USER;` |
| Active connections | `SELECT * FROM pg_stat_activity;` |
| Table size | `SELECT pg_size_pretty(pg_total_relation_size('employees'));` |
| Database size | `SELECT pg_size_pretty(pg_database_size(CURRENT_DATABASE()));` |
| Vacuum | `VACUUM employees;` |
| Analyze | `ANALYZE employees;` |
| Vacuum analyze | `VACUUM ANALYZE employees;` |
| Kill query | `SELECT pg_cancel_backend(pid);` |
| Terminate connection | `SELECT pg_terminate_backend(pid);` |
| Show configuration | `SHOW ALL;` |
| Set parameter | `SET work_mem = '64MB';` |

#### 24. psql terminal commands

These commands are used inside the PostgreSQL terminal (`psql`), not as normal SQL statements.

| Command | Purpose |
| --- | --- |
| `\l` | List databases |
| `\c company` | Connect to database |
| `\dt` | List tables |
| `\d employees` | Describe table |
| `\di` | List indexes |
| `\dv` | List views |
| `\df` | List functions |
| `\du` | List users and roles |
| `\dn` | List schemas |
| `\dp` | Show table permissions |
| `\x` | Toggle expanded output |
| `\timing` | Show query execution time |
| `\i file.sql` | Execute SQL file |
| `\o output.txt` | Save query output |
| `\q` | Exit PostgreSQL |
