---
uid: IS_OptionalParametersTab
---

# Optional parameters tab

<!-- This is an interface-specific skeleton topic. UPDATE WITH INFORMATION FOR YOUR INTERFACE. -->

![alt](https://link)

| Field | Description |
|:-|:-|
| **Write Size Cache (# of Events)** | When laboratory caching is enabled (/LB), specifies the maximum number of values written in one (bulk) call to the PI Archive; default is 10240 events per bulk. This parameter can be used to tune - (throttle) the load on the PI Server. (/WS=#, Default: 10240, Optional) |
| **Write Delay (milliseconds)** | When laboratory caching is enabled (/LB), specifies the write delay (in milliseconds) between bulk writes to the PI archive. Default is 10ms. Used to tune the load on the PI System and the - network. (/WD=#, Default: 10, Optional) |
| **Maximum Log (# of Files)** | Maximum number of log files in the circular buffer. The interface starts overwriting the oldest log files when the MAXLOG has been reached. By default, log files are never overwritten. (/- MaxLog=#, Optional) |
| **Maximum Log File Size (mb)** | Maximum size of the log file in MB. If this parameter is omitted, the default maximum is 20 MB. (/MaxLogSize=#, Default: 20, Optional) |
| **Consecutive Errors to Reconnect** | Number of consecutive errors that causes the interface to de-allocate all ODBC statements and attempt to reconnect to the RDBMS. (/ERC=#, Optional) |
| **Failover Timeout (seconds)** | Specifies how long to wait for query results to return before failing over to the secondary RDBMS server. (/Failover_Timeout=#, Optional) |
| **Direct SQL Execution** | All SQL statements are prepared, bound and executed each time they are scheduled for execution. By default, statements are prepared and bound only once, before the first execution. (/ExecDirect, Optional) |
| **Laboratory Caching** | Bulk-write events directly to PI Archive. When this option is enabled, the Location5 setting is ignored. Event handling is faster when this option is enabled, and archive mode is ARCREPLACE. (/- lb, Optional) |
| **Times are UTC** | Handle timestamps as UTC. If the timestamps in the RDBMS are stored in UTC format, you must enable this setting.(/UTC, Optional) |
| **No Input Errors** | Disable writing of the BAD_INPUT, IO_TIMEOUT digital states when an error occurs. (/NO_INPUT_ERROR, Optional) |
| **Read Before Overwrite** | Check the archive to see if value already exists at the same timestamp. If so, do not overwrite with new value. Affects only points with Location5=1. (/RBO, Optional) |
| **Exit Before Reconnect** | Exit if connection error occurs. By default, the interface tries to reconnect. (/EBR, Optional) |
| **Distribute Outside Point Source** | Enable interface to update points with point source other than the one configured for the interface instance. (/DOPS, Optional) |
| **Ignore Nulls** | Ignore events retrieved from the RDBMS if value is NULL.Prevents writing of the "No Data" system digital state for tag group and RxC distributions when the value column is NULL. (/Ignore_Nulls, - Optional) |
| **Scan Class - I/O Rate Tag fields** | Configure an I/O rate tag and assign a scan class to it. (/TF, Optional) |
