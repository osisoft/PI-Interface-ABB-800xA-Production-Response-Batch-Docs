---
uid: EquipmentArbitrationEventsUnavailable
---

# Equipment arbitration events unavailable

If the batch execution system does not generate equipment arbitration events, select the "Disable Arbitration" option (/noarbitration). Note that, without equipment arbitration events, the interface cannot precisely determine the start and end of unit batches.

If you disable arbitration, the interface determines the start time of unit batches using the timestamp of the "Unit Procedure Started" event or the start of the next operation or phase for the unit, whichever is later. For end time, the interface uses the timestamp from the "Unit Procedure Finished" event or the end of the last operation or phase for the unit, whichever is earlier.

For operation-level recipes, the interface uses the start time of the first phase as the start time for the parent operation and unit batch, and the timestamp of the "Operation Finished" message as the end time of the phase, operation and unit batch.
