
# 🛠️ Oracle Database Commands Cheat Sheet

A comprehensive guide for Oracle SQL and DBA tasks. Includes user management, performance tuning, backup, and real-world scripts—ideal for support engineers and interview prep.

---

## 📂 Sections
- User Management
- Table Management
- Tablespace Management
- Performance & Monitoring
- Backup and Recovery (RMAN)
- Export/Import (Data Pump)
- Scheduled Jobs
- PL/SQL Basics
- Index Management
- Constraints
- Views
- Synonyms
- Sequences
- Triggers
- Materialized Views
- Real-life DBA Scripts & Interview Tips
- Used for querying the database to retrieve data.

## 1. User Management

```sql
CREATE USER test_user IDENTIFIED BY password;
GRANT CONNECT, RESOURCE TO test_user;
REVOKE RESOURCE FROM test_user;
DROP USER test_user CASCADE;
```

**Use case**: Retrieving all employees in the HR department.

---

## 2. INSERT – Inserting Data

Used for adding new records to the table.

```sql
INSERT INTO employees (name, department, salary)
VALUES ('John Doe', 'Finance', 60000);
```

**Use case**: Adding a new employee to the database.

---

## 3. UPDATE – Modifying Data

Used to modify existing records in the database.

```sql
UPDATE employees
SET salary = 65000
WHERE name = 'John Doe';
```

**Use case**: Updating the salary of an employee.

---

## 4. DELETE – Removing Data

Used to delete records from the database.

```sql
DELETE FROM employees WHERE department = 'HR';
```

**Use case**: Deleting employees from the HR department.

---

## 5. CREATE TABLE – Creating a New Table

Used to create a new table in the database.

```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    department VARCHAR(50),
    salary DECIMAL(10, 2)
);
```

**Use case**: Creating an `employees` table to store employee information.

---

## 6. ALTER TABLE – Modifying Table Structure

Used to modify the structure of an existing table.

```sql
ALTER TABLE employees ADD COLUMN hire_date DATE;
```

**Use case**: Adding a `hire_date` column to the `employees` table.

---

## 7. DROP TABLE – Deleting a Table

Used to delete a table from the database.

```sql
DROP TABLE employees;
```

**Use case**: Deleting the `employees` table permanently.

---

## 8. JOIN – Combining Data from Multiple Tables

Used to retrieve data from multiple related tables.

```sql
SELECT employees.name, departments.department_name
FROM employees
INNER JOIN departments
ON employees.department_id = departments.id;
```

**Use case**: Displaying employee names and their department names.

---

## 9. INDEX – Speeding up Searches

Used to improve query performance on large tables.

```sql
CREATE INDEX idx_salary ON employees(salary);
```

**Use case**: Creating an index on the `salary` column to speed up queries.

---

## 10. TRANSACTION – Managing Multiple Operations

Ensures a group of operations are completed together or not at all.

```sql
BEGIN TRANSACTION;
UPDATE employees SET salary = salary + 5000 WHERE department = 'Finance';
DELETE FROM employees WHERE name = 'John Doe';
COMMIT;
```

**Use case**: Updating and deleting within a secure transaction.

---

## 11. GRANT – Giving Permissions

Used to provide access rights to a user.

```sql
GRANT SELECT, INSERT ON employees TO user1;
```

**Use case**: Granting permissions on the `employees` table to `user1`.

---

## 12. REVOKE – Revoking Permissions

Used to remove access rights from a user.

```sql
REVOKE SELECT, INSERT ON employees FROM user1;
```

**Use case**: Revoking access from `user1` on the `employees` table.

---

## 13. BACKUP DATABASE – Creating a Database Backup

Used to back up a database for data protection.

```sql
BACKUP DATABASE mydb TO DISK = 'C:\backup\mydb.bak';
```

**Use case**: Creating a backup of the `mydb` database.

---

## 14. RESTORE DATABASE – Restoring from Backup

Used to restore a database from a backup.

```sql
RESTORE DATABASE mydb FROM DISK = 'C:\backup\mydb.bak';
```

**Use case**: Restoring the `mydb` database from a backup.

---

> 📘 Feel free to contribute more real-life SQL examples!
