---
uid: IS_LocationFive
---

# **Location5** (<Interface-specific description>)

The **Location5** attribute configures exception reporting and the handling of events with duplicate timestamps. For output points, it configures how events are recovered from the PI Data Archive to a point source.

Tags and queries that include PI annotations bypass exception reporting and are written directly to the archive, regardless of their **Location5** attribute setting. Note that the interface also performs recovery during startup in real-time mode, to ensure that it captures any events that occurred during its downtime.

## Input points

To configure handling of out-of-order data for an input point, set **Location5** as follows:

| Value | Description |
|:-|:-|
| 0 | Enable standard exception reporting and out-of- order data handling for a tag. If the PI Data Archive already contains an event with the same time- stamp as the incoming event, the archived event - is not replaced with the incoming event. |
| 1 | Disable exception handling and send all incoming values to the snapshot. For out-of-order data, existing events are replaced and new events are added. |
| 2 | Archive all incoming out-of-order values. Be aware that if you set **Location5** to 2 , there can be multiple events with the same timestamp. |
| 3 | For the tag distribution and strategy, forward to PI only newer events than PI snapshot. |

## Output points

To configure handling of out-of-order data for an output point, set **Location5** as follows:

| Value | Description |
|:-|:-|
| -1 | Disable out-of-order data recovery for a tag (query is not executed) |
| 0 | Enable out-of-order data handling and output recovery for new events. Out of order data errors are logged as -109 errors in the PI message log. |
| 1 | Enable enhanced out-of-order data processing (per-event-type handling) |
