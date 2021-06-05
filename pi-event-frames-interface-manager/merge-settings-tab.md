---
uid: BIF_MergeSettingsTab
---

# Merge settings tab

The command line parameter settings on this tab configure merging of the batch generation, as described in the following table:

| Merge settings (Command line parameter settings) | Description |
| ------------------------------------------------ | ----------- |
| Merge operation (/MOP) | Merge identically-named operations under the same parent unit procedure. |
| Merge unit procedures (/MUP) | Merge identically-named sequential unit procedures running on the same unit into a single unit procedure. |
| Merge multiple source batches with same batch ID into one batch (/MERGE) |Enable merging of multiple source batches with same ID. The original data for each batch merged is stored in PI properties under a node named using the ID of the original batch. |
| Batch ID mask (/BIDM) | Override the incoming batch ID. |
| Truncate batch ID (/TBID) | Use the truncated batch ID in the batch ID field of unit procedures. |