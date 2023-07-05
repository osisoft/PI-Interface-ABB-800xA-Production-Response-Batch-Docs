---
uid: BIF_Propertytemplates
---

# Property templates 

To define properties (batch database) or attributes (PI AF) to be stored at a particular level of the batch hierarchy, you create property templates. The syntax for property templates is as follows:


```text
PROPERTY[<index>].<setting> = <value>
```

Instead of PROPERTY, you can specify ATTRIBUTE. The `<index>` is a unique identifier used to group the settings for a particular property. To include data from the data source, specify placeholders.

For example, if you define the following template:

```text
Property[1].Value=[Time]:[Descript]:[Pval]:[EU]-[Event]_Testing
```

...and the interface applies it to the following incoming data:

```text
[Time]="12/01/2015 12:01:05" [Descript]=abc [Pval]=123.456 [EU]=cm [Event]=Report
```

The following property is added to the resulting batch or batch-level event frame:

```text
12/01/2015 12:01:05:abc:123.456:cm-Report_Testing
```

## Property template settings

The following headings describe the settings required to define property templates.

### NAME 

(Optional) Specifies how the property is to be named. You can use an expression to configure the name, but note that the resulting name must be unique. If two different name templates generate the same name, the property value is overwritten and no error is logged. If you omit the name setting, the interface assigns a default name ("Event_n").

By default, properties are created at the level of the batch hierarchy that triggers their creation. To create a property at the top of the hierarchy, regardless of where it was triggered, specify "$" at the beginning of the expression that defines the name. 

For example: 

```text
Property[1].Name = $\[Event]
```

Additionally, you can use the not equals syntax ("!+") with anything that has a comparison. 

For example:

```text
Property[1].Trigger = [UNITPROCEDURE, value!=""]
Property[1].Trigger = [UNITPROCEDURE, value!="*"]
Property[1].Trigger = [UNITPROCEDURE, value!="aprefix"]
```

In this example, the property on the first UNITPROCEDURE placeholder triggers without meeting any condition. The second placeholder triggers with any value while the third triggers only if the condition equals "aprefix". 

**Valid Placeholders**

* [AREA]
* [BATCHID]
* [COMMENT]
* [DESCRIPT]
* [EU]
* [EVENT]
* [OPERATION]
* [PHASE]
* [PHASEMODULE]
* [PHASESTATE]
* [PHASESTEP]
* [PROCEDURE]
* [PROCESSCELL]
* [PVAL]
* [TIME]
* [UNIQUEID]
* [UNIT]
* [UNITPROCEDURE]
* [USERID] 
* [@.value="Exact Field"]
* [#.value="Field Mask"]
* [!.value="Example"]
* [?.value="Tag"]
* [*.value="Unit"]
* [Advanced parsing](../how-batch-interfaces-work/templates-for-mapping-data-source-events/placeholders-and-advanced-parsing.md)

### VALUE 

(Required) Specifies the value to be stored in the property. To compose the value, you can use free text plus valid placeholders.

Basic example:

```text
Property[1].Value = [BatchID] | event: <State*> | [Descript] | val: [Pval] 
```

Advanced parsing:

```text
Property[1].Value = [BatchID] | event: [*,value="State*"] | [Descript] | val: [Pval]
```

**Note:** For SQL data sources with the "Use original batch event view" option enabled (/UOBEV), you cannot use the [PVAL] or [EU] placeholders. To obtain this data you must parse it from the [DESCRIPT] placeholder.

Additionally, you can use the not equals syntax ("!+") with anything that has a comparison. 

For example:

```text
Property[1].Name = $\[Event, value!=""]
Property[1].Name = $\[Operation, value!=""]
```

**Valid Placeholders**

* [AREA]
* [BATCHID]
* [COMMENT]
* [DESCRIPT]
* [EU]
* [EVENT]
* [OPERATION]
* [PHASE]
* [PHASEMODULE]
* [PHASESTATE]
* [PHASESTEP]
* [PROCEDURE]
* [PROCESSCELL]
* [PVAL]
* [TAG]
* [TIME]
* [UNIQUEID]
* [UNIT]
* [UNITPROCEDURE]
* [USERID] 
* [@.value="Exact Field"]
* [#.value="Field Mask"]
* [!.value="Example"]
* [?.value="Tag"]
* [*.value="Unit"]
* [Advanced parsing](../how-batch-interfaces-work/templates-for-mapping-data-source-events/placeholders-and-advanced-parsing.md)

### TRIGGER 

Specifies the event that causes the interface to generate the property. To define a trigger, specify an expression composed of a placeholder and value. When the interface detects the specified value in the placeholder, it generates the property. 

Examples:

```text
Property[1].Trigger = [Parameter, value="State Ch*"]
```

```text
Property[1].Trigger = [Value, value="tes*"]
```

```text
Property[1].Trigger=[Event, value="State*] [Pval,value=RUNNING"]
```

```text
Property[1].Trigger=[Event]
```

Additionally, you can use the not equals syntax ("!+") with anything that has a comparison. 

For example:

```text
Property[1].Trigger = [UNITPROCEDURE, value!=""]
Property[1].Trigger = [UNITPROCEDURE, value!="*"]
Property[1].Trigger = [UNITPROCEDURE, value!="aprefix"]
```

In this example, the property on the first UNITPROCEDURE placeholder triggers without meeting any condition. The second placeholder triggers with any value while the third triggers only if the condition equals "aprefix". 

You can specify multiple triggers for a single property. If you specify the triggers on a single line, the property is generated only when all the conditions are met (logical AND). If you specify the trigger expressions on separate lines, the property is generated when any of the conditions is met (logical OR). 

Here is an example of a **logical AND** trigger where all conditions must be met:

```text
.TRIGGER=[Event, value=”Recipe Header”][Descript, value=”Description”][Value, value=”My Description”]
```

Conversely, the following is an example of a **logical OR** trigger. At least one of these conditions must be met:

```text
.TRIGGER=[COMMENT, value=""]
.TRIGGER=[EVENT, value=three]
.TRIGGER=[PHASESTATE, value=active]
.TRIGGER=[UNIT, value=S88]
```

**Valid Placeholders**

* [AREA]
* [BATCHID]
* [COMMENT]
* [DESCRIPT]
* [EU]
* [EVENT]
* [OPERATION]
* [PHASE]
* [PHASEMODULE]
* [PHASESTATE]
* [PHASESTEP]
* [PROCEDURE]
* [PROCESSCELL]
* [PVAL]
* [UNIQUEID]
* [UNIT]
* [UNITPROCEDURE]
* [USERID] 
* [@.value="Exact Field"]
* [#.value="Field Mask"]
* [!.value="Example"]
* [?.value="Tag"]
* [*.value="Unit"]
* [Advanced parsing](../how-batch-interfaces-work/templates-for-mapping-data-source-events/placeholders-and-advanced-parsing.md)

### TRANSLATE 

Specifies values for translation according to the translation map you define. Values set to `TRUE` are translated.

**Valid Placeholders**

* TRUE 
* FALSE

### TYPE

Specifies the data type for the value. To configure the interface to evaluate the data and assign the data type accordingly, specify **AUTO**.

**Valid Placeholders**

* STRING
* FLOAT
* INTEGER
* AUTO

### CATEGORY 

(AF only) Specifies the AF category to be assigned to the attribute.

**Valid Placeholders**

* [AREA]
* [BATCHID]
* [COMMENT]
* [DESCRIPT]
* [EU]
* [EVENT]
* [OPERATION]
* [PHASE]
* [PHASEMODULE]
* [PHASESTATE]
* [PHASESTEP]
* [PROCEDURE]
* [PROCESSCELL]
* [PVAL]
* [TIME]
* [UNIQUEID]
* [UNIT]
* [UNITPROCEDURE]
* [USERID] 
* [@.value="Exact Field"]
* [#.value="Field Mask"]
* [!.value="Example"]
* [?.value="Tag"]
* [*.value="Unit"]
* [Advanced parsing](../how-batch-interfaces-work/templates-for-mapping-data-source-events/placeholders-and-advanced-parsing.md)

### UOM or ENGUNITS or EU

Specifies the units of measure for the attribute. (See /UOBEV note for VALUE setting, above.)

**Valid Placeholders**

* [AREA]
* [BATCHID]
* [COMMENT]
* [DESCRIPT]
* [EU]
* [EVENT]
* [OPERATION]
* [PHASE]
* [PHASEMODULE]
* [PHASESTATE]
* [PHASESTEP]
* [PROCEDURE]
* [PROCESSCELL]
* [PVAL]
* [TIME]
* [UNIQUEID]
* [UNIT]
* [UNITPROCEDURE]
* [USERID] 
* [@.value="Exact Field"]
* [#.value="Field Mask"]
* [!.value="Example"]
* [?.value="Tag"]
* [*.value="Unit"]
* [Advanced parsing](../how-batch-interfaces-work/templates-for-mapping-data-source-events/placeholders-and-advanced-parsing.md)
