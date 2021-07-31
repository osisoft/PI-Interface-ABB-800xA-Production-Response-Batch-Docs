---
uid: BIF_Databases
---

# Databases

[!include[interface](../includes/product-short.md)] is a manufacturing execution system that generates consumable log files in the form of Event Journal Files (EVT files). [!include[interface](../includes/product-short.md)] collects data from those EVT files.

A single interface instance can collect data from multiple [!include[interface](../includes/product-short.md)] sources by configuring the interface to read EVT files from multiple locations.

## Event Journals

Event journals are text files in which the BES logs batch events. For the [!include[interface](../includes/product-short.md)] systems, the interface expects each line in the event journal to be composed of the following tab-delimited fields, in the order specified:

```
[TIMESTAMP] [BATCHID] [RECIPE] [DESCRIPT] [EVENT] [PVALUE] [EU] [AREA] [PROCCELL] [UNIT] [PHASE] [PHASEDESC] [USERID] [UNIQUEID] [COMMENT]
```
    
In event journals, the product ID information is stored in the [PVALUE] field, in the row that contains the description "Product Code". Typically this is a recipe header event. If the BES indicates the product ID using a value other than "Product Code," you must translate the value to "Product Code" to ensure that the interface detects it. To configure the translation using PI Event Frame Interface Manager, check the Translation field on the template's Configuration tab and specify the source and target string on the Translations dialog.
