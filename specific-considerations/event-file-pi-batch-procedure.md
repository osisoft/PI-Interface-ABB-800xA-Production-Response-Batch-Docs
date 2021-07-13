---
uid: BIF_EventFilePIBatchProcedure
---

# Event file PIbatch procedure

## Event journal start/end events

### Start

[EVENT] = "System Message" and [PVALUE] = "Beginning Of BATCH"

### End

Either of these events end a batch:

* [EVENT] = "System Message" and [PVALUE] = "End Of BATCH"

Or

* [EVENT] = "State Change" and [PVALUE] field = "REMOVED", "COMPLETE" or "ABORTED"
