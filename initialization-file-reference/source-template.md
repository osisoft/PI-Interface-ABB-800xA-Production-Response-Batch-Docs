---
uid: BIF_sourcetemplatesettings
---

# Source templates

A single interface instance can gather data from one or more data sources. In the .ini file, each data source is assigned an index, which is used to specify the settings for the data source. To specify a setting for a data source, use the following syntax:

```text
Source[<index>].<setting> = <value>
```

Following are some simple examples of data source templates.

Single DeltaV Batch Historian:

```text
Source[1].sqlserver = deltav10 Source[1].database = DVHisDB
```

DeltaV Batch Historian plus Alarms and Events:

```text
Source[1].sqlserver = deltav10 Source[1].database = DVHisDB Source[2].sqlserver = deltav10\DELTAV_CHRONICLE Source[2].database = Ejournal Source[2].isAE = true
```

## Data source template parameters

The following headings describe the parameters for data source templates.

### `cursor= client | server` 

Optional for SQL data source. Available in DeltaV 9.3+.

* Client (default): The interface retrieves complete dataset prior to processing. High memory consumption on interface node.
* Server: The interface requests and processes one dataset record at a time. Reduces interface node memory consumption.

### `evtdir=<path>`

Required for event file data sources. This parameters defines the folder that contains the event files. 

Example:

```text
Source[1].evtdir = D:\TEST\RELEASE\test_1
``` 

### `excludestates=<list>`

(Optional) Specifies a comma-separated list of phase states to ignore. Not case-sensitive. You can use wildcards for matching. 

Examples:

```text
excludestates=COMPLETED,AB*ING,IDLING, COMPLE*
```

### `isAE=true`

Indicates that the data source is a DeltaV Alarms and Events server.

### `opcnode=<node name or IP address>`

Required for OPC alarms and events data source. Available in DeltaV 10.3 and higher. Specifies the host of the DeltaV OPCAE server is installed. If used with DeltaV SQL server, must be defined for the same source. 

Example:

```text
Source[1].sqlserver = deltav10
Source[1].sqldatabase = DVHisDB
Source[1].opcnode = deltav10
Source[1].opcserver = DeltaV.OPCEventServer.1
```

### `opcserver=<server name>`

Optional for OPC alarms and events data source. Specifies the name of the alarms and events server, if you are not using the default server.

### `skipphases=<list>`

(Optional) Specifies a comma-separated list of phases to ignore. Not case-sensitive. You can use wildcards for matching. The interface checks the list against the [Phase] field (batch recipe) or [PhaseModule] field (equipment). 

Examples:

```text
skipphases=phase_1, ph*2,ph_test*, ph*ort*
```

### `skiprecipes=<list>`

(Optional) Specifies a comma-separated list of recipes to ignore. Not case-sensitive. You can use wildcards for matching. The interface checks the list against the corresponding event field, depending on recipe type, as follows:

```text
skiprecipes=recipe_1, rec*2,PRC_PAINT*, UP_TEST:2
```

### `skipunits=<list>`

(Optional) Specifies a comma-separated list of units to ignore. Not case-sensitive. You can use wildcards for matching. The interface checks the list against the corresponding [Unit] field. 

Example:

```text
skipunits = unit_1, u*2
```

### `sqlserver=<node name or IP address>`

Required for SQL Server data source. Specifies the host where SQL Server is running. Available in DeltaV 9.3+.

### `sqldatabase=<database name>`

Optional for SQL Server data source. Specifies the name of the database, if you are not using the default database. (DVHisDB).

### `sqlpswd=<password>` 

For explicit login to SQL Server. Enter the password for the `sqluser` parameter.

### `sqluser=<user name>` 

For explicit login to SQL Server. Use this parameter with `sqlpswd`. 

**Note:** By default the interface uses Windows authentication to connect to SQL Server. 
