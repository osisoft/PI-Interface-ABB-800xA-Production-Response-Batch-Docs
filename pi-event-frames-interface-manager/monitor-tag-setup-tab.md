---
uid: BIF_MonitorTagSetupTab
---

# Monitor Tag Setup tab

<!-- Batch Interface Framework Topic -->

From the **Monitor Tag Setup** tab, you can disable monitor tags for the [!include[interface](../includes/product-long.md)] that you do not use. Each batch interface supports approximately 40 tags, with each tag licensed in groups. Disabling unused tags reduces license consumption. Select each tag that you want to disable.

## Monitor tag options

To enable or disable tags in bulk, use the **Select all tags** and **Unselect all tags** options at the top of the window.

| Option | Description |
|--|--|
| Select all tags | Disables all monitor tags listed. |
| Unselect all tags | Activates all monitor tags previously disabled. |
| Monitor tag time window in days | Most monitor tags show a sum of events over a number of days. This setting allows the size of the window to be adjusted. The default value is one day. |

## Monitor tag reference 

The following table lists each monitor tag that you can disable from the **Monitor Tag Setup** tab.

| Monitor Tag | Point Type | Archiving<sup>1</sup> | Description |
|--|--|--|--|
| BatchStatus | Int32 | true | Status of interface data collection. |
| BatchProcessorStatus | Int32 | true | Status of interface data processing. |
| BatchListCount | Int32 | false | Number of objects in the cache. |
| EquipmentCount | Int32 | false | Number of equipment objects in the cache. |
| TagListCount | Int32 | false | Number of cached tags. |
| TagAEListCount | Int32 | false | Number of alarm and event tags. |
| EventReadCount | Int32 | false | Number of events processed. |
| ErrorCount | Int32 | false | Global error counter. |
| SourceUnitCount | Int32 | false | Number of unit modules found on source. |
| PIUnitCount | Int32 | false | Number of unit modules found on and added to destination. |
| SourcePhaseModCount | Int32 | false | Number of phase modules found on source. |
| PIPhaseModCount | Int32 | false | Number of phase modules found on and added to destination. |
| SourceBatchCount | Int32 | false | Number of batches found on source. |
| PIBatchCount | Int32 | false | Number of batches found on and added to destination. |
| SourceUnitBatchCount | Int32 | false | Number of unit batches found on source. |
| PIUnitBatchCount | Int32 | false | Number of unit batches found on and added to destination. |
| SourceSubBatchCount | Int32 | false | Number of sub batches found on source. |
| PISubBatchCount | Int32 | false | Number of sub batches found on and added to destination. |
| SourcePropertyNodeCount | Int32 | false | Number of property nodes found on source. |
| PIPropertyNodeCount | Int32 | false | Number of property nodes found on and added to destination. |
| SourcePropertyEventCount | Int32 | false | Number of property events found on source. |
| PIPropertyEventCount | Int32 | false | Number of property events found on and added to destination. |
| SourceTagCount | Int32 | false | Number of tags found on source. |
| PITagCount | Int32 | false | Number of tags found on and added to destination. |
| SourceTagEventCount | Int32 | false | Number of tag events found on source. |
| PITagEventCount | Int32 | false | Number of tag events found on and added to destination. |
| SourceTagAliasCount | Int32 | false | Number of tag aliases found on source. |
| PITagAliasCount | Int32 | false | Number of tag aliases found on and added to destination. |
| CachedBatchCount | Int32 | false | Number of batches in cache. |
| OpenBatchCount | Int32 | false | Number of open batches in cache. |
| SourceReadTime | Float32 | false | Time spent reading source data per iteration. |
| TagCacheTime | Float32 | false | Time spent updating the tag cache per event. |
| BatchCacheTime | Float32 | false | Time spent updating the batch cache per event. |
| EquipmentCacheTime | Float32 | false | Time spent updating the equipment cache per event. |
| BatchSyncTime | Float32 | false | Time spent synching with PI and AF per event list. |
| TagSyncTime | Float32 | false | Time spent synching tags per event list. |
| EquipmentSyncTime | Float32 | false | Time spent synching equipment per event list. |
| TotalTime | Float32 | false | Total time spent caching and synching batches, tags, and equipment per event list. |
| WaitingForEquipmentUB | Int32 | false | Number of unit batches waiting for unit defining events. |
| NumberOfWorkOrders  <!-- PASX Only --> |    Int32 |   false | Number of Work Orders being processed.|
| NumberofOpenWorkOrders <!-- PASX Only --> |   Int32 |   false | Number of Open Work Orders Being Processed.|
| WorkOrderQueryTimeAvg  <!-- PASX Only --> | Float32 | false | WorkOrder Query Time Average.|

<sup>1</sup>: Indicates whether the point that is created archives past values.

**Note:** The following monitor tags cannot be disabled:

* DeviceStatus
* HeartBeat
