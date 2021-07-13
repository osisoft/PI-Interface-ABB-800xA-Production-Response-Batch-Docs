---
uid: BIF_EventFilePIBatchUnitProcedure
---

# Event file PIUnitBatch unit procedure

## Event journal start/end events

### Start

For procedure- and unit procedure-level recipes, the interface requires both a start event and an "equipment acquired" event, as follows:

* [EVENT] = "System Message" and [DESCRIPT] field = "Unit Procedure Started"

And

* [EVENT] field = "Recipe Arbitration", [DESCRIPT] field = "Resource Acquired by recipe" and [EU] field = "Unit". The [PVALUE] field contains the actual unit name.
The latest timestamp is used as the start time for the unit batch.

Operation and phase-level recipes create parent batches and unit batches automatically. Operation-level recipes require a start event and an "equipment acquired" event. Phase-level recipes set the unit batch start time from the event that starts the phase; no equipment acquisition event is required.

### End

For procedure- and unit procedure-level recipes, the interface requires both an end event and an "equipment released" event, as follows:

* [EVENT] = "System Message" and [DESCRIPT] field = "Unit Procedure Finished".

And

* [EVENT] = "System Message" and [DESCRIPT] field = "Unit Procedure Finished".

And

* [EVENT] field = "Recipe Arbitration", [DESCRIPT] field = "Resource Released by recipe" and [EU] field = "Unit". The [PVALUE] field contains the actual unit name.
The earliest timestamp is used as the end time.

Operation-level recipes require an end event and an "equipment released" event. Phase-level recipes set the unit-batch end time from the event that ends the phase; no equipment release event is required.

## SQL server start/end events

### Start

To start a unit batch, the interface requires both a "start" event and an "equipment acquired" event. It uses the latest timestamp as the start time for the unit batch. Specifically, the interface scans for the following events:

* The batch recipe event containing the [STARTTIME] timestamp associated with the specific "unitprocedure" object retrieved from the batchrecipeview view.

* The arbitration event containing the [ACQUIRETIME] timestamp associated with the specific unit arbitration object retrieved from the batchequipmentview view.

Operation- and phase-level recipes create parent batches and unit batches automatically. Operation-level recipes require a "start" event and an "equipment acquired" event. Phase-level recipes set the unit batch start time from the event that starts the phase; no equipment acquisition event is required.

For operation-level recipes, the following two events are required to start a unit batch:

* The batch recipe event containing the [STARTTIME] timestamp associated with the operation retrieved from the batchrecipeview view.

* The arbitration event containing the [ACQUIRETIME] timestamp associated with the unit arbitration event retrieved from the batchequipmentview view.

The latest timestamp is used as the start time.

For phase-level recipes, the start time is set using the [STARTTIME] field of the batch recipe associated with the phase object.

### End

To end a unit batch, the interface requires both an "end" event and an "equipment released" event. It uses the earliest timestamp as the end time for the unit batch. Specifically, the interface scans for the following events:

* The batch recipe event containing the [ENDTIME] timestamp associated with the specific "unitprocedure" object retrieved from the "batchrecipeview" view.

* The arbitration event containing the [RELEASETIME] timestamp associated with the specific unit arbitration object retrieved from the batchequipmentview view.

For operation-level recipes, the following two events are required to end a unit batch:

* The batch recipe event containing the [STARTTIME] timestamp associated with the operation retrieved from the batchrecipeview view.

* The arbitration event containing the [ACQUIRETIME] timestamp associated with the unit arbitration event retrieved from the batchequipmentview view.

The earliest timestamp is used as the end time.

For operation-level recipes, the following two events are required to end a unit batch:

* The batch recipe event containing the [STARTTIME] timestamp associated with the operation retrieved from the batchrecipeview view.

* The arbitration event containing the [ACQUIRETIME] timestamp associated with the unit arbitration event retrieved from the batchequipmentview view.

The earliest timestamp is used as the end time.

For phase-level recipes, the end time is set using the [ENDTIME] field of the batch recipe associated with the phase object.
