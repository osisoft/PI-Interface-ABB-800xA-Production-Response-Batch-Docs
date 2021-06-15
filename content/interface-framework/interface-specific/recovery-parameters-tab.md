---
uid: IS_RecoverParametersTab
---

# Recovery parameters tab

<!-- Draft comment: INTERFACE-SPECIFIC: Replace with content for your interface. -->

## Recovery Mode

Enable/disable recovery mode.

## Input Processing

| Field | Description |
|:-|:-|
| **Recovery Start Time** | Specifies the point in time at which recovery begins. Can be an absolute time, a relative time, or the name of a PI timestamp tag. ( /RECOVERY_TIME ) Optional |
| **Recovery End Time** | Specifies the point in time at which recovery ends. Can be an absolute time, a relative time, or the name of a PI timestamp tag. (/RECOVERY_TIME ) Optional |
| **Input Recovery Step** | Specifies the size of chunk in which data is read during recovery, to avoid taxing system resources. Optional |

## Output Processing

| Field | Description |
|:-|:-|
| **Recovery Start Time** | Specifies the point in time at which recovery begins. (/RECOVERY_TIME ) Optional |
| **Recovery End Time** | Specifies the point in time at which recovery ends.(/RECOVERY_TIME ) Optional |
| **Out of Order Options** | Specifies how out-of-order data is to be handled, for tags with Location5 set to 1. (/OOO_OPTIONS) Optional |
