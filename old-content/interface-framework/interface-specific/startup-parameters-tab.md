---
uid: IS_StartupParametersTab
---

# Startup parameters tab

<!-- Draft comment: INTERFACE-SPECIFIC: Replace with content for your interface. -->

## File Locations

| Field | Description |
|:-|:-|
| **Interface Log File** | Full path to the interface specific log file. (/OUTPUT) Optional |
| **SQL Files Directory** | Directory of the SQL statement files. (/SQL) Optional |
| **Global Variables Files** | Full path to the global SQL variable file. (/GLOBAL) Optional |

## DSN Settings

| Field | Description |
|:-|:-|
| **DSN** | Data Source Name (/DSN) Required |
| **Username** | Username for access to RDBMS (/USER_ODBC) Required |
| **Password** | Password for access to RDBMS (/PASS_ODBC). The password is encrypted and stored locally in the directory configured for interface log files (/OUTPUT). To enter a new password, click ![alt](https://link) |

## Successful - Status Range

Specify the range of digital states indicating success from the system digital state table.

| Field | Description |
|:-|:-|
| Start Code | Enter the starting location in the system digital state table. (/SUCC1=#) Optional |
| End Code | Enter the ending location in the system digital state table (/SUCC2=#) Optional |

## Bad Input - Status Range

Specify the range of digital states indicating Bad Input from the system digital state table.

| Field | Description |
|:-|:-|
| Start Code | Enter the starting location in the system digital state table. (/BAD1=#) Optional |
| End Code | Enter the ending location in the system digital state table (/BAD2=#) Optional |
