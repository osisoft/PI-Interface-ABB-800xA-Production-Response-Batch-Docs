---
uid: BIF_StartAndStopEvents
---

# Start and stop events

<!-- Customized for ABB 800xA -->

The interface determines the recipe hierarchy from the History response stream and reads allocated equipment from the RESOURCE_response stream. The start and end time of the task with levelnumber = 1 is read from the BatchStartTime and BatchEndTime variables in the Variable Response stream. The start and end times of other tasks are read from the Event Response stream, and the recipe name is read from the Variable Response stream.

Variable Response stream: The start and end times of other tasks are read from the Event Response stream, while the recipe name is read from the Variable Response stream.

This batch interface provides two options for determining how the hierarchy of batch events is stored in the PI System:

## Default

The interface constructs a four-level hierarchy, using Batch_phase tasks to determine the lowest level. If equipment is allocated at level 2, the level 1 event is treated as the procedure level and level 2 is treated as the unit procedure level, level 3 as the operation level, and Batch_phase tasks as the phase level. If equipment is allocated at level 1, the interface treats level 1 as the unit procedure level and generates a parent procedure. In this case, level 2 is treated as the operation level, and Batch_phase tasks as the phase level. In both cases, any levels between the operation level and the level at which the Batch_phase tasks occur are not collected by the interface.

## BATCHRCP Enabled

The interface preserves the parent/child structure of the events in ABB rather than using Batch_phase tasks to determine the lowest level of the hierarchy. Again, the interface treats the level at which equipment is allocated as the unit procedure level, so if equipment is associated with level 1, the interface generates a parent procedure level, and if equipment is allocated at level 2, level 1 is treated as the procedure level. The interface generates a maximum of six levels (procedure, unit procedure, operation, phase, phase state and phase step).
