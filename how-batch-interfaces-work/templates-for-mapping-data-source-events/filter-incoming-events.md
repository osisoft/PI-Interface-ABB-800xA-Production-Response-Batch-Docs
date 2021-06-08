---
uid: BIF_FilterIncomingEvents
---

# Filter incoming events

You can configure filters to restrict the interface from processing certain events. You can filter out data based on its level in the batch hierarchy and on its unit. The interface examines fields in incoming events for the specified data and, if it matches, the event is not processed. 

1. To exclude incoming data from processing using PI Event Frames Interface Manager, go to the Filters tab.

2. Expand the setting for the type of data that you want to filter (phases, units, recipes or phase states).

3. Specify the data that you want to exclude.

    You can use wildcards to define masks for matching.
