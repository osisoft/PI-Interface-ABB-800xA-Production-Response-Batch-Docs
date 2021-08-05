---
uid: BIF_EventFilePhaseState
---

# Event file Phase State

## Event journal start/end events

The event containing [EVENT] = "State Change" and [PVALUE] field = <State Name> indicates a new phase state.

## SQL server start/end events

The interface reads the name of the new phase state from the [ACTION] column in the brecipestatechangeview or batcheventview view.
