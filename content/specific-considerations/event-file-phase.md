---
uid: BIF_EventFilePhase
---

# Event file phase

## Event journal start/end events

### Start

For recipes that run at or above the phase level, the event containing [EVENT] = "State Change" and [PVALUE] field = "RUNNING".

### End

For recipes that run at or above the phase level, the event containing [EVENT] = "State Change" and [PVALUE] field = "COMPLETE" / "STOPPED" / "ABORTED" ends a phase.

## SQL server start/end events

### Start

For operation- and higher-level recipes, the interface sets the start time for a phase using [STARTTIME] timestamp from the phase start event retrieved from the batchrecipeview view. For phase-level recipes, the interface starts a parent operation using the timestamp from the first phase start event ([EVENTTYPE] = "State Change" and [EVENTDESCRIPT] contains "RUNNING").

### End

For operation- and higher-level recipes, the interface sets the end time for a phase using [ENDTIME] timestamp from the phase end event retrieved from the batchrecipeview view. For phase-level recipes, the interface ends a parent operation using the timestamp from the first phase end event ([EVENTTYPE] = "State Change" and [EVENTDESCRIPT] = "COMPLETE", "STOPPED" or "ABORTED").
