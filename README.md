
# 🛠️ Oracle Database Commands Cheat Sheet

A comprehensive guide for Oracle SQL and DBA tasks. Includes user management, performance tuning, backup, and real-world scripts—ideal for support engineers and interview prep.

---

## 📂 Sections
- [User Management](#1-User-Management)
- [Table Management](#2-Table-Management)
- [Tablespace Management](#3-Tablespace-Management)
- [Performance & Monitoring](#4-Performance-Monitoring)
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

## 12. Synonyms


```sql
CREATE SYNONYM emp FOR employees;
DROP SYNONYM emp;
```

---

## 13. Sequences



```sql
CREATE SEQUENCE emp_seq START WITH 1 INCREMENT BY 1;
INSERT INTO employees VALUES (emp_seq.NEXTVAL, 'Mike', 5500);
```

---

## 14.  Triggers


```sql
CREATE OR REPLACE TRIGGER emp_bi
BEFORE INSERT ON employees
FOR EACH ROW
BEGIN
  :NEW.salary := NVL(:NEW.salary, 3000);
END;
/
```

---

## 15. Materialized Views


```sql
CREATE MATERIALIZED VIEW emp_mv AS SELECT * FROM employees;
```

---

## 16. Real-life DBA Scripts


```sql
SELECT SUM(BYTES)/1024/1024/1024 AS SIZE_GB FROM DBA_DATA_FILES;
SELECT OBJECT_NAME, OBJECT_TYPE FROM DBA_OBJECTS WHERE STATUS='INVALID';
SELECT SEGMENT_NAME, BYTES/1024/1024 AS SIZE_MB FROM USER_SEGMENTS WHERE SEGMENT_TYPE='TABLE';

SELECT s.sid, s.serial#, p.spid, s.username, s.program, t.value AS cpu_usage
FROM v$session s, v$process p, v$sesstat t, v$statname n
WHERE s.paddr = p.addr AND s.sid = t.sid AND t.statistic# = n.statistic#
AND n.name = 'CPU used by this session'
ORDER BY t.value DESC;

SELECT a.username, b.used_ublk*8192/1024/1024 AS undo_size_mb
FROM v$transaction b, v$session a
WHERE a.saddr = b.ses_addr;

SELECT l.session_id, o.object_name, o.object_type
FROM v$locked_object l, dba_objects o
WHERE l.object_id = o.object_id;

SELECT * FROM SESSION_PRIVS;
SELECT LOG_MODE FROM V$DATABASE;

-- Archive mode enable (manual)
-- SHUTDOWN IMMEDIATE
-- STARTUP MOUNT
-- ALTER DATABASE ARCHIVELOG;
-- ALTER DATABASE OPEN;

SELECT SEGMENT_NAME, SEGMENT_TYPE, TABLESPACE_NAME, BYTES/1024/1024 MB
FROM DBA_SEGMENTS
ORDER BY BYTES DESC;

-- lsnrctl status
SELECT * FROM DBA_ROLE_PRIVS WHERE GRANTED_ROLE = 'DBA';
```

---

> 👨‍💻 Author
> Bhavesh
> 📜 License
> Free to use and share — Attribution appreciated!

