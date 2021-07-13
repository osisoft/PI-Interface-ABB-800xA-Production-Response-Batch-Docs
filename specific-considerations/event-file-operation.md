---
uid: BIF_EventFileOperation
---

# Event file operation

## Event journal start/end events

### Start

For recipes that run at or above the operation level, the event containing [EVENT] = "System Message" and [DESCRIPT] = "Operation Started" and [RECIPE] = "Operation" indicates the start of an operation.

For phase-level recipes, the event containing [EVENT] = "State Change" and [PVALUE] = "RUNNING" indicates the start of an operation.

### End

For recipes that run at or above the operation level, the earlier of the following events ends the operation:

* The event containing [EVENT] = "System Message" and [DESCRIPT] field = "Operation Finished"

Or

* The event containing [EVENT] = "State Change" and [PVALUE] field = "REMOVED" and [RECIPE] = "Operation".

For phase-level recipes, the interface assigns the operation start time from the batch recipe event containing [EVENT] = "State Change" and [PVALUE] = "RUNNING".

## SQL server start/end events

### Start

For operation- and higher-level recipes, the interface sets the start time for an operation using the [STARTTIME] timestamp from the operation start event retrieved from the batchrecipeview view. For phase-level recipes, the interface starts a parent operation using the timestamp from the first phase start event ([EVENTTYPE] = "State Change" and [EVENTDESCRIPT] contains "RUNNING"). The event is retrieved from the brecipestatechangeview or batcheventview view.

### End

For operation- and higher-level recipes, the interface sets the end time for an operation using [ENDTIME] timestamp from the operation end event retrieved from the batchrecipeview view. For phase-level recipes, the interface ends a parent operation using the timestamp from the first phase end event ([EVENTTYPE] = "State Change" and [EVENTDESCRIPT] contains "COMPLETE", "ABORTED" or "STOPPED". The event is retrieved from the brecipestatechangeview or batcheventview views.
