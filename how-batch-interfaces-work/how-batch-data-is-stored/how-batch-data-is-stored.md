---
uid: HowBatchDataIsStored
---

# How batch data is stored

Batch interfaces support two options for storing batch data: as PI batches or as PI AF event frames. For PI batches, the interface represents equipment (units) by creating PI modules. For event frames, the interface represents equipment by creating PI AF assets. The batch database is a special-purpose database, optimized for (and constrained by) S88 and similar models, whereas PI AF event frames and elements provide a highly flexible, general-purpose structure that enables you to define your asset model and event hierarchy as needed. Most notably, the batch database imposes a one-unit-batch-per-unit restriction, whereas event frames do not restrict the number of unit batches that can be active in the same unit at the same time.
