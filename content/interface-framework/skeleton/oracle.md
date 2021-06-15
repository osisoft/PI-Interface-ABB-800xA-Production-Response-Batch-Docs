---
uid: SK_Oracle
---

# Oracle

The caveats in this section are known to apply to Oracle7.0;
Oracle 8.x, 9i, 10g, 11g;
and Oracle RDB.

## Open statements limitation

Some versions of Oracle permit a maximum of 100 open concurrently-prepared statements. The RDBMS issues one SQL statement per tag, so each interface instances can service 100 tags concurrently. If the limit is exceeded, the following error is logged:

[S][HY000]: [Oracle][ODBC][Ora]ORA-01000: maximum open cursors exceeded

The limit can also be exceeded by cursors that are opened in stored procedures.

You can increase this limit for your Oracle server by editing the INIT.ORA file and setting OPEN_CURSORS. However, this is a server-level configuration change, so undertake it with care. As an alternative, consider the following approaches:

* Use tag grouping.
* Run multiple instances of the interface.
* Enable direct execution: In PI ICU, on the rdbodbc > Optional Parameters tab, check Direct SQL Execution.

## Limiting the number of rows returned

To reduce CPU usage, you can limit the number of rows returned by a query using the LIMIT TO clause.

### Example for Oracle RDB

```text
SELECT timestamp,value,status FROM table1 LIMIT TO 10 ROWS;
SELECT timestamp,value,status FROM table1 LIMIT TO 10 ROWS
WHERE timestamp > ? ORDER BY timestamp;
```

### Example for Oracle 8.0 (NT) and above

```text
SELECT timestamp,value,status FROM table1 WHERE ROWNUM<11;
```

## Returning results from stored procedures

To create a stored procedure that returns results, you must create the stored procedure and a package, as follows:

### Creating the package

To define a package, issue the CREATE PACKAGE statement. For example:

```text
CREATE OR REPLACE PACKAGE myTestPackage IS
TYPE gen_cursor IS REF CURSOR; END myTestPackage;
```

### Creating the stored procedure

The following example stored procedure selects rows with a timestamp later than the date argument specified as an input parameter.

```text
CREATE OR REPLACE PROCEDURE myTestProc (cur OUT myTestPackage.gen_cursor, ts IN date) 
IS res myTestPackage.gen_cursor; BEGIN
OPEN res FOR SELECT pi_time,pi_value,0 FROM pi_test1
WHERE pi_time > ts; cur := res; END myTestProc;
```

### Calling the stored procedure

To execute the stored procedure, issue the following query:

```text
{CALL myTestProc(?)}; P1=TS
```
