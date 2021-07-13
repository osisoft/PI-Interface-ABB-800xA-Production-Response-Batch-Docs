---
uid: BIF_EventFilePhaseStep
---

# Event file phase step

By default, phase steps are not detected. You must enable phase steps and configure the strings that indicate state changes. Unlike other levels, no end events are recorded for phase steps: the start of a phase step ends the preceding one.

## Event journal start/end events

### Start

The event containing [EVENT] = "Report" and [DESCRIPT] or [PVALUE] field = <Start Substring> starts a phase step. The name of the phase step is parsed from the text in the [DESCRIPT] or [PVALUE] field.

### End

The event containing [EVENT] = "Report" and [DESCRIPT] or [PVALUE] field = <End Substring> ends a phase step. The name of the phase step is parsed from the text in the [DESCRIPT] or [PVALUE] field.

## SQL server start/end events

### Start

The event containing [EVENTTYPE] = "Report" and [EVENTDESCR] field = <Start Substring> starts a phase step. The name of the phase step is parsed from the text in the [EVENTDESCR] field.

### End

The event containing [EVENTTYPE] = "Report" and [EVENTDESCR] field = <End Substring> ends a phase step. The name of the phase step is parsed from the text in the [EVENTDESCR] field.
