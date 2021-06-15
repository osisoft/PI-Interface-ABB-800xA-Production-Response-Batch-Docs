---
uid: SK_MicrosoftSQLServe
---

# Microsoft SQL Server

## Use the DateTime data type

For PI timestamps, use the _DateTime_ data type. Do not use the SQL Server _Timestamp_ data type, which is a database-wide unique number that cannot be bound to the interface time- related placeholders such as TS, LST, and so on.

## Limit the number of rows returned

To specify the maximum number of rows to be returned, include the TOP clause. For example:

```text
SELECT TOP 10 timestamp, value, status FROM table1;
```

## Stored procedures: avoiding Invalid Cursor State Error

If a stored procedure contains more complex code, such as a combination of INSERT and SELECT statements, issue the SET NOCOUNT ON statement before issuing the queries, to ensure that queries return only data, minus the status information that is usually included. By default, statements like INSERT, UPDATE, DELETE, {CALL} return the number of affected rows, which, when combined with the result set from a SELECT statement, can cause the following errors:

```text
"[S][24000]: [Microsoft][ODBC SQL Server Driver]Invalid cursor state" 
"[S][HY000]: [Microsoft][ODBC SQL Server Driver]Connection is busy with results for another hstmt"
```

Example:

```text
CREATE PROCEDURE sp_RDBMSPI1(@name varchar(30),@TS datetime) AS
SET NOCOUNT ON
INSERT table1 VALUES(@name, @TS)
SELECT timestamp, value,0 FROM table2
WHERE Tagname = @name and timestamp > @TS
```
