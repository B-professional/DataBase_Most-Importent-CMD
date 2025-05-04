
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

---

## 2. Table Management

```sql
CREATE TABLE employees (
  id NUMBER PRIMARY KEY,
  name VARCHAR2(100),
  salary NUMBER
);
INSERT INTO employees VALUES (1, 'John', 5000);
UPDATE employees SET salary = 6000 WHERE id = 1;
DELETE FROM employees WHERE id = 1;
DROP TABLE employees;
```


---

## 3. Tablespace Management


```sql
CREATE TABLESPACE myspace DATAFILE 'myspace.dbf' SIZE 100M AUTOEXTEND ON;
ALTER TABLESPACE myspace ADD DATAFILE 'myspace2.dbf' SIZE 50M;
DROP TABLESPACE myspace INCLUDING CONTENTS AND DATAFILES;
```


---

## 4. Performance & Monitoring

```sql
SELECT SID, SERIAL#, USERNAME, STATUS FROM V$SESSION;
ALTER SYSTEM KILL SESSION 'SID,SERIAL#';
SELECT * FROM V$SESSION_LONGOPS;
SELECT * FROM V$SYSSTAT;
```


---

## 5.  Backup and Recovery (RMAN)

```sql
-- RMAN TARGET /
BACKUP DATABASE;
BACKUP TABLESPACE users;
RESTORE DATABASE;
RECOVER DATABASE;
```

---

## 6. Export/Import using Data Pump


```sql
expdp system/password FULL=Y DIRECTORY=dpdump DUMPFILE=full.dmp LOGFILE=full.log
impdp system/password FULL=Y DIRECTORY=dpdump DUMPFILE=full.dmp LOGFILE=imp.log
```

---

## 7.  Scheduled Jobs

```sql
BEGIN
  DBMS_SCHEDULER.CREATE_JOB (
    job_name        => 'my_job',
    job_type        => 'PLSQL_BLOCK',
    job_action      => 'BEGIN NULL; END;',
    start_date      => SYSTIMESTAMP,
    repeat_interval => 'FREQ=DAILY; BYHOUR=1',
    enabled         => TRUE
  );
END;
/
```


---

## 8. PL/SQL Basics


```sql
BEGIN
  DBMS_OUTPUT.PUT_LINE('Hello, World!');
END;
/

DECLARE
  v_name VARCHAR2(50);
BEGIN
  v_name := 'Oracle';
  DBMS_OUTPUT.PUT_LINE(v_name);
END;
/
```


---

## 9. Index Management

```sql
CREATE INDEX emp_name_idx ON employees(name);
DROP INDEX emp_name_idx;
```


---

## 10. Constraints


```sql
ALTER TABLE employees ADD CONSTRAINT emp_pk PRIMARY KEY (id);
ALTER TABLE employees ADD CONSTRAINT dept_fk FOREIGN KEY (dept_id) REFERENCES departments(id);
ALTER TABLE employees DROP CONSTRAINT emp_pk;
```


---

## 11. Views



```sql
CREATE VIEW emp_view AS SELECT id, name FROM employees;
DROP VIEW emp_view;
```

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
