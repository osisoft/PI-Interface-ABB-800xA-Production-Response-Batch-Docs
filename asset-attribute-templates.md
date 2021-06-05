---
uid: BIF-asset-attribute-template
---

# Asset attribute template

The Asset Attribute associates data from the data source with a desired element. To create properties, you define Asset Attribute templates on the **Templates** page of the **PI Event Frame Interface Manager**. The Asset Attribute templates specify the data to be extracted. Placeholders, wildcards, and advanced parsing features enable you to extract precisely the desired data from the events that the interface reads from the data source.

| Setting | Description |
|--|--|
| Index | Unique numeric ID (integer). |
| Name | Attribute name. Every attribute name under the same element must be unique. If the template does not define a name, the interface assigns a default name of "Event_&lt;_n_&gt;", where &lt;_n_&gt; is a unique integer. To write attribute at the top level regardless of the level from which the triggering event originated, specify the @ symbol as the first element in name path as follows: `>@\[Parameter]`. |
| Value | Value to assign to attribute. |
| Trigger | The event that triggers the generation of the attribute. Updates can be triggered by the data source or by PI events such as the start or end of a recipe level. |
| Translate | Specifies whether the attribute is to be translated before being written to the PI System. Specify true or false (default is false). |
| EngUnits | Engineering units. |
| Type | **INTEGER**, **FLOAT**, **STRING** (Default), **FLOATSTRING**, **AUTO**. If **Type** is set to **AUTO**, the interface assigns the data type based on the first item of data that it receives. If the first value received is an integer but subsequent values are floating point, the interface creates an integer attribute or property and truncates any subsequent floating point values before storing them. To avoid truncating numeric input that includes a mix of integer and floating point values, specify **FLOATSTRING** rather than **AUTO**. |
| Category | Category |
| UOM | Unit of measure. To map the units of measure in the data source to the correct PI AF engineering units, check the UOM check box and configure the mapping between the source units of measure and the units available in PI AF. |
| Descriptor | Descriptor |
| ALLOWEMPTYVALUE | True = T will allow an attribute to be created with an empty value. |
| TAGPATH | A full path to a PI Tag: `\\MyServer\Sinusoid`. This will cause the attribute to be a data reference to the PI tag indicated. An attribute can have a Value or a TagPath. If it has both, then the Value will be used. |
| ASSETPATH | There can be multiple paths an asset can be configured to follow. |

## Template example one 

Asset Attribute that has a value: 

```text
ASSETATTRIBUTE[1].ASSETPATH=[REFERENCECATEGORY]\[REFERENCE]
ASSETATTRIBUTE[1].CATEGORY=[ATTRIBUTECATEGORY]
ASSETATTRIBUTE[1].VALUE=[VALUE]
ASSETATTRIBUTE[1].DESCRIPTOR=[ATTRIBUTEDESC]
ASSETATTRIBUTE[1].ENGUNITS=[ATTRIBUTEUOM]
ASSETATTRIBUTE[1].TYPE=AUTO
ASSETATTRIBUTE[1].TRIGGER=[EVENT,value="ELEMENT ATTRIBUTE"]
ASSETATTRIBUTE[1].ALLOWEMPTYVALUE=T
```

## Template example two

Asset Attribute that has a tagpath: 

```text
ASSETATTRIBUTE[5].NAME=[ATTRB1]
ASSETATTRIBUTE[5].ASSETPATH=[REFERENCECATEGORY]\[REFERENCE]
ASSETATTRIBUTE[5].CATEGORY=[ATTRIBUTECATEGORY]
ASSETATTRIBUTE[5].TAGPATH="\\MyServer\[DATAREFERENCE,delim="/",count=4]"
ASSETATTRIBUTE[5].DESCRIPTOR=[ATTRIBUTEDESC]
ASSETATTRIBUTE[5].ENGUNITS=[ATTRIBUTEUOM]
ASSETATTRIBUTE[5].TYPE=AUTO
ASSETATTRIBUTE[5].TRIGGER=[EVENT,value="ELEMENT ATTRIBUTE"][ATTRIBUTEDATTYPE,value="TagPath"]
ASSETATTRIBUTE[5].ALLOWEMPTYVALUE=T
```
