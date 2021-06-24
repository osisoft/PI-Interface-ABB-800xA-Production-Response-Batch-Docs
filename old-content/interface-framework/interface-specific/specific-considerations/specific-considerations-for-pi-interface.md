---
uid: IS_SpecificConsiderations
---

# Specific considerations for PI Interface for <interface name>

<!-- Draft comment: This is an interface-specific topic. REPLACE WITH CONTENT FOR YOUR INTERFACE. -->

Despite the use of ODBC to insulate the interface from variations in RDBMS implementations, some differences occur. ODBC drivers differ in their implementation of the standard, and relational databases differ in functionality, data type support, SQL syntax and so on. Known RDBMS-specific considerations are discussed, but be advised that other differences are certain to exist.

## Oracle

The caveats in this section are known to apply to Oracle7.0; Oracle 8.x, 9i, 10g, 11g; and Oracle RDB.

### Open statements limitation

Some versions of Oracle permit a maximum of 100 open concurrently-prepared statements. The RDBMS issues one SQL statement per tag, so each interface instances can service 100 tags concurrently. If the limit is exceeded, the following error is logged:

[S][HY000]:[Oracle][ODBC][Ora]ORA-01000: maximum open cursors exceeded

The limit can also be exceeded by cursors that are opened in stored procedures.

You can increase this limit for your Oracle server by editing the INIT.ORA file and setting OPEN_CURSORS. However, this is a server-level configuration change, so undertake it with care. As an alternative, consider the following approaches:

* Use tag grouping.
* Run multiple instances of the interface.
* Enable direct execution: In PI ICU, on the rdbodbc > Optional Parameters > tab, check Direct SQL Execution.

### Limiting the number of rows returned

To reduce CPU usage, you can limit the number of rows returned by a query using the LIMIT TO clause. For example:

#### Oracle RDB

```text
SELECT timestamp,value,status FROM table1 LIMIT TO 10 ROWS;
SELECT timestamp,value,status FROM table1 LIMIT TO 10 ROWS
WHERE timestamp > ? ORDER BY timestamp;
```

#### Oracle 8.0 (NT) and above

```text
SELECT timestamp,value,status FROM table1 WHERE ROWNUM<11;
```

### Returning results from stored procedures

To create a stored procedure that returns results, you must create the stored procedure and a package, as follows:

#### Creating the package

To define a package, issue the CREATE PACKAGE statement. For example:

```text
CREATE OR REPLACE PACKAGE myTestPackage IS
TYPE gen_cursor IS REF CURSOR; END myTestPackage;
```

#### Creating the stored procedure

The following example stored procedure selects rows with a timestamp later than the date argument specified as an input parameter.

```text
CREATE OR REPLACE PROCEDURE myTestProc (cur OUT myTestPackage.gen_cursor, ts IN date)
IS res myTestPackage.gen_cursor; BEGIN
OPEN res FOR SELECT pi_time,pi_value,0 FROM pi_test1
WHERE pi_time > ts; cur := res; END myTestProc;
```

#### Calling the stored procedure

To execute the stored procedure, issue the following query:

```text
{CALL myTestProc(?)}; P1=TS
```

## Microsoft SQL Server

### Use the DateTime data type

For PI timestamps, use the DateTime data type. Do not use the SQL Server Timestamp data type, which is a database-wide unique number that cannot be bound to the interface time- related placeholders such as TS, LST, and so on.

### Limiting the number of rows returned

To specify the maximum number of rows to be returned, include the TOP clause. For example:

```text
SELECT TOP 10 timestamp, value, status FROM table1;
```

Stored procedures: avoiding Invalid Cursor State Error

If a stored procedure contains more complex code, such as a combination of INSERT and SELECT statements, issue the SET NOCOUNT ON statement before issuing the queries, to ensure that queries return only data, minus the status information that is usually included. By default, statements like INSERT, UPDATE, DELETE, {CALL} return the number of affected rows, which, when combined with the result set from a SELECT statement, can cause the following errors:

```text
"[S][24000]: [Microsoft][ODBC SQL Server Driver]Invalid cursor state"
"[S][HY000]: [Microsoft][ODBC SQL Server Driver]Connection is busy with results for another hstmt"
```

Example:

```text
CREATE PROCEDURE sp_RDBMSPI1 (@name varchar(30),@TS datetime) AS
SET NOCOUNT ON
INSERT table1 VALUES(@name, @TS)
SELECT timestamp, value,0 FROM table2
WHERE Tagname = @name and timestamp > @TS
```
