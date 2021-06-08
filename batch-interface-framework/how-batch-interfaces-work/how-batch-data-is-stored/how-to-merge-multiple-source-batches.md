---
uid: HowToMergeMultipleSourceBatches
---

# How to merge multiple source batches

To merge multiple source batches that have identical batch IDs, enable the **Merge multiple source batches with same batch ID into one PI batch** option on the **Merge Setup** tab of the PI Event Frame Interface Manager. To ensure that related batch IDs match, you can configure a batch ID mask that extracts a common substring from the incoming ID. The interface caches batches and, when it reads a new batch from the source, it checks its cache for a batch with a matching ID. If a match is found, the interface merges the batches. If no match is found in the cache, the interface creates a new batch. By default, the interface caches batches for one day. To configure the cache duration, go to the **Time Settings** tab and set the **Cache time** value.

## Configuring the Batch ID for Merging Multiple Batches

To enable the interface to merge multiple incoming source batches into a single batch, you must ensure that the batch IDs are identical. To override the default batch ID that the interface reads from the data source, you can configure a batch ID mask that extracts a common substring of the incoming ID to be used as the batch ID. The mask must match a contiguous substring from the incoming batch ID (that is, you cannot define a mask that skips characters). To configure the mask using PI Event Frame Interface Manager as follows: on the **Merge Setup** tab, set the **Batch ID mask** field. Specify the mask using fixed text and the following wildcards:

| Wildcard | Description                       |
|----------|-----------------------------------|
| `#`      | Single digit numerical value, 0-9 |
| `@`      | Single alpha character, a-z, A-Z  |
| `?`      | Any single symbol                 |
| `!`      | Repeat the previous mask symbol   |
| `*`      | Any set of symbols                |

You can specify multiple masks as a comma-separated list. The interface uses the result from the first mask that successfully generates a substring. If the interface cannot match the mask to the data in the incoming field, the entire field is used. As an example, for a data source BatchID column that contains the text `lot30112 / 90dev123 / 12345stp / ld567`, the following table lists masks and results:

| Mask | Result | Matches… |
|--|--|--|
| `#####` | 30112 | The first five contiguous digits. The first matching substring is used. |
| `###` | 301 | The first three contiguous digits. |
| `@@@#####` | lot30112 | Five contiguous digits with three contiguous characters and the characters are placed before the sequence of digits. |
| `##@@@###` | 90dev123 | Five contiguous digits with three contiguous characters and the characters are placed before the third digit. |
| `#####@@@` | 12345stp | Five contiguous digits with three contiguous characters and the characters are followed the digits. |
| `?????` | lot30 | The first five characters, regardless of type. |
