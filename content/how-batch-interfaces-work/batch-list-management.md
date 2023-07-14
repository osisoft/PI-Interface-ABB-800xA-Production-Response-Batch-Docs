---
uid: BIF_batchlistmanagement
---

# Batch list management

In real-time mode, the interface first checks to see if there are batches in the batch list. If there are no batches in the batch list after querying between the query start and end time, the start time remains the same for the next query. 

If there are only closed batches in the list, the interface selects the batch with the most recent start time for the Next Query Start Time. If that time falls after the Current Query Start Time, it will be used as the Next Query Start Time. If the time does not fall after the Current Query Start Time, the Next Query Start Time remains the same.

If there are open batches in the list, the interface selects the batch with the most recent start time for the Next Query Start Time from the list of open batches. If that time falls after the Current Query Start Time, it will be used as the Next Query Start Time. If the time does not fall after the Current Query Start Time, the Next Query Start Time remains the same. 

In history recovery mode, the configuration of the [Maximum query time frame (/MAXQTF=)](../pi-event-frames-interface-manager/time-settings-tab.md) on the Time Settings tab determines the query end time. For example, if the MAXQTF is set to five days, the end time for the queries moves forward five days from the query start time. When the interface defines a query start time, the end time moves forward automatically based on the MAXQTF configuration. 
