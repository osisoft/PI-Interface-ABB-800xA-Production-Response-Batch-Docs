---
uid: BIF_PropertyTemplatesEFIM
---

# Property templates

Properties associate data from the data source with a desired level of the batch or event frame hierarchy. To create properties, you define property templates on the Templates page of the PI Event Frame Interface Manager. The property templates specify the data to be extracted and the level of the hierarchy at which they are created. Placeholders, wildcards and advanced parsing features enable you to extract precisely the desired data from the events that the interface reads from the data source.
With event frames, properties (AF attributes) can be created at any level of the batch hierarchy. However, in the batch database, properties are stored only at the top (procedure or batch) level of the batch hierarchy. This top-level collection of properties includes the properties for the lower levels of the batch hierarchy, arranged according to level.
To define a property template on the Templates page of the PI Event Frame Interface Manager, configure the following settings:

| Setting | Description |
| ------- | ----------- |
| Index | Unique numeric ID (integer). |
| Name | Property name. Every event name under the same node must be unique. If the template does not define a name, the interface assigns a default name of "Event_<n>", where <n> is a unique integer. To write properties at the top level regardless of the level from which the triggering event originated, specify the @ symbol as the first element in name path as follows: @\[Parameter]. To write properties under the UniqueID property (PI Batch only), regardless of the level from which the triggering event originated, specify the $ symbol as the first element in name path, as follows: $\[Parameter].|
| Value | Value to assign to property. |
| Create property | Specifies the level at which the property is to be created. Options are as follows: |
|   |  * At recipe level: By default, properties are created at the recipe level corresponding to the level in the data source from which the data was read. |
|   |  * Under root node: Create properties at the top level of the batch or event frame hierarchy, regardless of the level at which they originated.
|   |  * Under UniqueID node: (Batch database only, not event frames) Create properties under the batch's UniqueID node. |
| Data type | PI data type of the value. Note that if the incoming value is incompatible with the specified type, the event is not processed, and an error is logged. |
| Trigger | The event that triggers the generation of the property. Updates can be triggered by the data source or by PI events such as the start or end of a recipe level. |
| Translate | Specifies whether the property is to be translated before being written to the PI System. Specify true or false (default is false). |
| EngUnits (AF only) | Engineering units |
| Type | INTEGER, FLOAT, STRING (Default), FLOATSTRING, AUTO. If Type is set to AUTO, the interface assigns the data type based on the first item of data that it receives. If the first value received is an integer but subsequent values are floating point, the interface creates an integer attribute or property and truncates any subsequent floating point values before storing them. To avoid truncating numeric input that includes a mix of integer and floating point values, specify FLOATSTRING rather than AUTO. |
| Category (AF only) | Asset category |
| UOM (AF only) | Unit of measure. To map the units of measure in the data source to the correct PI AF engineering units, check the UOM check box and configure the mapping between the source units of measure and the units available in PI AF. |
| Descriptor (AF only) | Description. |
| Tagpath | The path to a PI Server tag. For example: \\MyPIServer\sinusoid. This will create an attribute that has a data reference to a PI point. |
| Allowemptyvalue | If true, the attribute will be created with an empty value. If false, and the value is empty, the attribute will not be created. |
| Examples | Examples |

To create or update a property named **TestTagCalc** that contains a ten-day total for the "sinusoid" tag and a ten-day minimum for the "test_data_1" tag, configure the template with the following settings:

| Setting | Set to |
| ------- | ------ |
| Name | TestTagCalc |
| Value | total:[Tag, name="sinusoid", range="10d", func="TOTAL"] |
| Trigger | [Event,value="PIEVENT"] [Descript,value="BATCH"] [Pval,value="START"] |

To populate the product property with the formula name when a "Recipe header" event arrives, ignoring undefined product codes, use the following settings:

| Setting | Set to |
| ------- | ------ |
| Product | [PVAL] |
| ProductTrigger | [EVENT,VALUE="Recipe Header"] [DESCRIPT,VALUE="Product Code"] [PVAL, VALUE!="UNDEFINED"] |
| ProductTrigger | [EVENT,VALUE="Formula Header"] [DESCRIPT,VALUE="Formula Name"] |