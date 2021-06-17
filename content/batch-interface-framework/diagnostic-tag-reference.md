---
uid: BIF_DiagnosticTagReference
---

# Diagnostic tag reference

Performance tags, which are automatically created for each instance of the interface, enable you to monitor the performance of the instance. There are 35 performance tags, categorized as follows:

* Health monitoring
* Object counters
* Timers

## Health monitoring tags

There are two tags designed to monitor the health of the interface: the **HeartBeat** tag and the **DeviceStatus** tag. The HeartBeat tag is updated with the scan frequency configured for the interface or 60 seconds, whichever is less. The value of the HeartBeat tag is a cycle of integers from 1 to 15. The device status tag is automatically created and configured by the interface on startup. The device tag reflects status as follows:

* **"Good":** The interface is properly communicating and reading data from the data sources.
* **"1 | Starting":** The interface is executing its initialization routines.
* **"2 | <details>":** Indicates successful connection to the data source.
* **"3 | <details>":** Indicates failure to access the event journal file directory or failure to read data from the event journal file.

The properties of health monitoring tags are provided in the table below, where the Prefix represents <Interface>_<ID>. Note, if these tags do not exist. the interface creates them automatically during startup.

| Tag name | Point Type | Loc1 | Loc3 | PointSource | ExcDesc |
| -------- | ---------- | ---- | ---- | ----------- | ------- |
| Prefix_DeviceStatus | Int32 | Intf ID | 0 | Intf Pt Src | [UI_DEVSTAT] |
| Prefix_HeartBeat | Int32 | Intf ID | 1 | Intf Pt Src | [UI_HEARTBEAT] |

## Object counter tags

The first time it is started, the interface creates 24 tags designed to monitor its performance. Archiving flag for these tags is turned off. The following table contains common point attributes for this group of tags:

| Point type | Location1 | Point source |
| ---------- | --------- | ------------ |
| Int32 | <Interface ID> | <Interface Point Source> |

The attributes for each performance counter tag are provided in the table below where the Prefix is defined as _<Interfaceid>. All counters are set to 0 when the interface starts up.

| Tag Name | Loc3 | ExcDesc | Description |
| -------- | ---- | ------- | ----------- |
| <interfaceID>_EventReadCount | 2 | [UI_EVENTREADCOUNT] | Number of events read from the source since startup. |
| <interfaceID>_ErrorCount | 3 | [UI_ERRORCOUNT] | Number of errors since startup. |
| <interfaceID>_SourceUnitCount | 4 | [UI_SOURCEUNITCOUNT] | Number of units found on the data source(s) since startup. |
| <interfaceID>_PIUnitCount | 5 | [UI_PIUNITCOUNT] | Number of units added since startup. |
| <interfaceID>_SourcePhaseModCount | 6 | [UI_SOURCEPHASEMODCOUNT] | Number of phase modules found on the data source(s) since startup. |
| <interfaceID>_PIPhaseModCount | 7 | [UI_PIPHASEMODCOUNT] | Number of phase modules added since startup. |
| <interfaceID>_SourceBatchCount | 8 | [UI_SOURCEBATCHCOUNT] | Number of batches found on the data source(s) since startup. |
| <interfaceID>_PIBatchCount | 9 | [UI_PIBATCHCOUNT] | Number of batches added since startup. |
| <interfaceID>_SourceUnitBatchCount | 10 | [UI_SOURCEUNITBATCHCOUNT] | Number of unit batches found on the data sources(s) since startup. |
| <interfaceID>_PIUnitBatchCount | 11 | [UI_PIUNITBATCHCOUNT] | Number of unit batches added since startup. |
| <interfaceID>_SourceSubBatchCount | 12 | [UI_SOURCESUBBATCHCOUNT] | Total number of operations, phases, and phase states found on the data source since startup. |
| <interfaceID>_PISubBatchCount | 13 | [UI_PISUBBATCHCOUNT] | Total number of operations, phases, and phase states added since startup. |
| <interfaceID>_SourcePropertyNodeCount | 14 | [UI_SOURCEPROPNODECOUNT] | Number of property nodes found in data source(s) since startup. |
| <interfaceID>_PIPropertyNodeCount | 15 | [UI_PIPROPNODECOUNT] | Number of PIProperty objects (nodes) added since startup. |
|<interfaceID>_SourcePropertyEventCount | 16 | [UI_SOURCEPROPEVENTCOUNT] | Number of events to be written to the batch properties found on the data source(s) since startup. |
| <interfaceID>_PIPropertyEventCount | 17 | [UI_PIPROPEVENTCOUNT] | Number of PIProperties (events) added since startup. |
| <interfaceID>_SourceTagCount | 18 | [UI_SOURCETAGCOUNT] |Number of tags found on the data source(s) since startup |
| <interfaceID>_PITagCount | 19 | [UI_PITAGCOUNT] | Number of PI tags added since startup. |
| <interfaceID>_SourceTagEventCount | 20 | [UI_SOURCETAGEVENTCOUNT] | Number of events to be written into tags found on the data sources(s) since startup. |
| <interfaceID>_PITagEventCount | 21 | [UI_PITAGEVENTCOUNT] | Number of events written into PI points since startup. |
| <interfaceID>_SourceTagAliasCount | 22 | [UI_SOURCETAGALIASCOUNT] | Number of tag aliases to be created based on the data source(s) since startup. |
| <interfaceID>_PITagAliasCount | 23 | [UI_PITAGALIASCOUNT] | Number of PI aliases added since startup. |
| <interfaceID>_CachedBatchCount | 24 | [UI_CACHEDBATCHCOUNT] | Number of batch objects cached in the local memory. |
| <interfaceID>_OpenBatchCount | 25 | [UI_OPENBATCHCOUNT] | Subset of cached objects that have no end time set. |
| <interfaceID>_WaitingForEquipmentUB | 34 | [UI_UBWAITFOREQUIP] | Number of unit batches that do not have equipment allocated yet. |

## Timers

The last performance tag category is composed of timer tags, which are built automatically on first interface startup. Each timer tag reports on how much time per scan it took the interface to perform a particular task. There are three categories of timer tag: data source reading, local data caching and synchronizing cached data with the PI System.

| TagName | Loc3 | ExcDesc | Description |
| ------- | ---- | ------- | ----------- |
| <interfaceID>_SourceReadTime | 26 | [UI_SOURCEREADTIME] | The time per scan it took the interface to read data from data source(s). |
| <interfaceID>_TagCacheTime | 27 | [UI_TAGCACHETIME] | The time per scan it took the interface to populate local tag cache. |
| <interfaceID>_BatchCacheTime | 28 | [UI_BATCHCACHETIME] | The time per scan it took the interface to populate the local batch cache. |
| <interfaceID>_EquipmentCacheTime | 29 | [UI_EQUIPCACHETIME] | The time per scan it took the interface to populate the local equipment (module) cache. |
| <interfaceID>_BatchSyncTime | 30 | [UI_BATCHSYNCTIME] | The time per scan it took the interface to synchronize local batch cache with the PI System. |
| <interfaceID>_TagSyncTime | 31 | [UI_TAGSYNCTIME] | The time per scan it took the interface to synchronize local tag cache with the PI System. |
| <interfaceID>_EquipmentSyncTime | 32 | [UI_EQUIPSYNCTIME] | The time per scan it took the interface to synchronize local equipment cache with the PI System. |
| <interfaceID>_TotalTime | 33 | [UI_TOTALTIME] | The total time per scan it took to read data, cache it in local memory and synchronize the local cache with the PI System. |