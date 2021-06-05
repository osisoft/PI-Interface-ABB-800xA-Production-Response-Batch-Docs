---
uid: BIF_HowBatchInterfacesWork
---

# How PI interfaces for batch and manufacturing execution systems work

Batch interfaces scan a data source for events of interest, such as the start or end of a level, and the acquisition and release of equipment.

Based on these events, the interface generates entries in the PI Batch Database or event frames. To handle configurations in which multiple batch execution systems manage related batch processes that you want to merge, you can configure a single interface instance to read multiple data sources.
