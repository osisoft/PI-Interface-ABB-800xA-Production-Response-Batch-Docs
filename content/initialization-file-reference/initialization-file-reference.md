---
uid: BIF_InitializationFileReference
---

# Initialization file reference

<!-- Customized for ABB 800xA. -->

The initialization (.ini) file stores configuration information for an interface instance. The PI Event Frame Interface Manager configuration tool generates and updates this file each time you edit the instance configuration. You can access initialization files from [!include[programdata](../includes/dir-long.md)]. 

**Note:** Before release 4.x, initialization files were stored in the interface installation directory.

**Tip:** To ensure a valid .ini file, use the PI Event Frame Interface Manager configuration tool. Do not edit the .ini file manually.

Use this appendix to learn about the contents of the .ini file for troubleshooting purposes.

The .ini file contains the following sections:

* **COMMAND LINE PARAMETERS:** Defines basic interface settings.
* **SIMPLE SWITCHES:** Defines connection settings.
* **SOURCE TEMPLATE:** Defines the settings required to connect to the data source and events to be skipped (filtered)
* **RECIPE TEMPLATE:** Defines how data is recorded at each level of the batch hierarchy.
* **TAG TEMPLATE:** Defines how tags are created and updated based on incoming data from the data source.
* **PROPERTY TEMPLATE:** Define how PI properties or event frame attributes are created based on incoming data from the data source.
* **TRANSLATIONS:** Maps text from the data source language to the target language for the PI System.
* **DCS LINK TEMPLATE:** Define rules for linking event frames created by different interfaces.

In defining settings for templates, you can use the following wildcards to compose expressions:

| Wildcard | Description |
| -------- | ----------- |
| # | single digit numerical value (0-9) |
| @ | single alphabetic character (a-z, A-Z) |
| ? | any single character |
| ! | repeat previous mask symbol |
| * | any number of characters |

## Source template settings

A single interface instance can gather data from one or more data sources. In the .ini file, each data source is assigned an index, which is used to specify the settings for the data source. To specify a setting for a data source, use the following syntax:

```text
Source[<index>].<setting> = <value>
```
    
**Note:** The `<index>` value is always 1. This interface only connects to a single MOM Services (S95PRIncrementer).

The following is an example of a data source template:

```text
ABB Ability MOM Services (S95PRIncrementer):
[SOURCE TEMPLATE]
SOURCE[1].USER=abbuser
SOURCE[1].PASSWORD=test12345$
SOURCE[1].CONNECTIONSTRING="wss://10.40.160.59:10940/SDS"
SOURCE[1].IS95PRACCESSOR=S95PR
SOURCE[1].INCREMENTORID=OSIInc
SOURCE[1].DATASOURCE=PR_OL
SOURCE[1].ROWLIMIT=1000 
```

<!-- MB 6/11/21: Adding content for ABB 800xA below -->

The following headings list the settings for data source templates used for this interface.

### `connectionstring=<URL>`
    
Required. 

The URL used to connect to ABB MOM Services. The encryption binding in the application server (such as WSS) and the hostname are used. Contact your ABB 800xA Administrator for additional guidance if needed.

### `DATASOURCE=<Data Source>`
    
Required.

Name of the Data Source. This is typically set to "PR_OL". Contact your ABB 800xA Administrator for additional guidance if needed.

### `INCREMENTORID=< Subscription ID >`
    
Required.

ID of the Incrementor used to subscribe for any task information. This is not specific to any ABB setting, and can be completely defined by the interface administrator.

### `IS95PRACCESSOR=<Type of service>`
    
Required.

ID of the IS95PRACCESSOR. This is typically set to "S95PR". Contact your ABB 800xA Administrator for additional guidance if needed.

### `password=<password>`
    
Required.

The password for the user defined above. This will be encrypted by PI Event Frames Interface Manager. Contact your ABB 800xA Administrator for additional guidance if needed.

### `ROWLIMIT=<Increment Size>`
    
Required.

Maximum number of rows that should be returned at one time from ABB MOM Services.

### `user=<ABB User>`
    
Required.

The user name required to explicitly login to ABB Ability MOM Services. Contact your ABB 800xA Administrator for additional guidance if needed.

## Property template settings

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

### Available property template settings

The following headings describe the settings required to define property templates.

### NAME 

(Optional) Specifies how the property is to be named. You can use an expression to configure the name, but note that the resulting name must be unique. If two different name templates generate the same name, the property value will be overwritten and no error is logged. If you omit the name setting, the interface assigns a default name ("Event_n").

By default, properties are created at the level of the batch hierarchy that triggers their creation. To create a property at the top of the hierarchy, regardless of where it was triggered, specify "$" at the beginning of the expression that defines the name. 

For example: 

```text
Property[1].Name = $\[Event]
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
* [TIME]
* [UNIQUEID]
* [UNIT]
* [UNITPROCEDURE]
* [USERID] 
* [*,value="Exact Field"]
* [*,value="Field Mask"]
* advanced parsing

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

* [*,value="Exact Field"]
* [*,value="Field Mask"]
* advanced parsing

### TRIGGER 

Specifies the event that causes the interface to generate the property. To define a trigger, specify an expression composed of a placeholder and value. When the interface detects the specified value in the placeholder, it generates the property. You can specify multiple triggers for a single property. If you specify the triggers on a single line, the property is generated only when all the conditions are met (logical AND). If you specify the trigger expressions on separate lines, the property is generated when any of the conditions is met (logical OR). 

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
* [*,value="Exact Field"]
* [*,value="Field Mask"]
* advanced parsing

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
* [*,value="Exact Field"]
* [*,value="Field Mask"]
* advanced parsing

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

* [*,value="Exact Field"]
* [*,value="Field Mask"]
* advanced parsing

## Tag templates

Tag template specify how the interface creates and updates PI tags based on incoming data. For example, the following template creates one tag per unit for state change events:

```text
Tag[1].Name=BESName:[UNIT].Event.[EVENT] 
Tag[1].Descriptor=[UNIT] [EVENT] 
Tag[1].EngUnits=[EU] 
Tag[1].Value=[DESCRIPT]|[EVENT]|[PVAL]|[EU]|[AREA]|[PROCESSCELL]|[UNIT]|[PHASEMODULE]|[USERID] 
Tag[1].Type=string Tag[1].UnitAlias=Event.[EVENT] 
Tag[1].Trigger=[EVENT,value="State Change"]
```

The following table lists valid settings for tag templates. The timestamp for tag events is taken from the triggering event.

### ANNOTATION 

Annotate the tag using a string.

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
* [PROCEDURE]
* [PROCESSCELL]
* [PVAL]
* [UNIQUEID] 
* [UNIT]
* [UNITPROCEDURE]
* [USERID]
* [*,value="Exact Field"]
* [*,value="Field Mask"]
* advanced parsing

### ANNOTATION2 

Annotate the tag using a name/value object.

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
* [PROCEDURE]
* [PROCESSCELL]
* [PVAL]
* [UNIQUEID] 
* [UNIT]
* [UNITPROCEDURE]
* [USERID]
* [*,value="Exact Field"]
* [*,value="Field Mask"]
* advanced parsing

## DESCRIPTOR 

Specifies how the descriptor field of the tag is populated.

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
* [PROCEDURE]
* [PROCESSCELL]
* [PVAL]
* [UNIQUEID] 
* [UNIT]
* [UNITPROCEDURE]
* [USERID]
* [*,value="Exact Field"]
* [*,value="Field Mask"]
* advanced parsing

### EU 

Specifies the engineering units for the tag.

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
* [PROCEDURE]
* [PROCESSCELL]
* [PVAL]
* [UNIQUEID] 
* [UNIT]
* [UNITPROCEDURE]
* [USERID]
* [*,value="Exact Field"]
* [*,value="Field Mask"]
* advanced parsing

### NAME

Specifies how the tag is to be named.

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
* [PROCEDURE]
* [PROCESSCELL]
* [PVAL]
* [UNIQUEID] 
* [UNIT]
* [UNITPROCEDURE]
* [USERID]
* [*,value="Exact Field"]
* [*,value="Field Mask"]
* advanced parsing
 
### PHASEALIAS

Configures the naming convention for the phase module alias generated by the interface. The unit alias refers to the MDB module or AF asset representing the phase module associated with the incoming event.

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
* [PROCEDURE]
* [PROCESSCELL]
* [PVAL]
* [UNIQUEID] 
* [UNIT]
* [UNITPROCEDURE]
* [USERID]
* [*,value="Exact Field"]
* [*,value="Field Mask"]
* advanced parsing

### TRIGGER

Specifies the event that causes the interface to generate or update the tag. To define a trigger, specify an expression composed of a placeholder and value. When the interface detects the specified value in the placeholder, it generates or updates the tag. You can specify multiple triggers for a single tag. If you specify the triggers on a single line, the tag is generated only when all the conditions are met (logical AND). If you specify the trigger expressions on separate lines, the tag is generated when any of the conditions is met (logical OR).

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
* [PROCEDURE]
* [PROCESSCELL]
* [PVAL]
* [UNIQUEID] 
* [UNIT]
* [UNITPROCEDURE]
* [USERID]
* [*,value="Exact Field"]
* [*,value="Field Mask"]
* advanced parsing

### TRANSLATE 

To translate the value according to the translation map that you define, set to TRUE.

**Valid Placeholders**

* TRUE
* FALSE

### TYPE

Specifies the data type for the tag. To configure the interface to evaluate the data and assign the data type accordingly, specify AUTO.

**Valid Placeholders**

* STRING
* FLOAT
* INTEGER
* AUTO

### UNITALIAS 

Configures the naming convention for the unit alias generated by the interface. The unit alias refers to the MDB module or AF asset representing the unit associated with the incoming event.

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
* [PROCEDURE]
* [PROCESSCELL]
* [PVAL]
* [UNIQUEID] 
* [UNIT]
* [UNITPROCEDURE]
* [USERID]
* [*,value="Exact Field"]
* [*,value="Field Mask"]
* advanced parsing

### VALUE

(Required) Specifies the value to be stored in the tag. To compose the value, you can use free text plus valid placeholders.

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
* [PROCEDURE]
* [PROCESSCELL]
* [PVAL]
* [TAG]
* [TIME]
* [UNIQUEID] 
* [UNIT]
* [UNITPROCEDURE]
* [USERID]
* [*,value="Exact Field"]
* [*,value="Field Mask"]
* advanced parsing

## Recipe templates

To define the data generated for each level of the batch hierarchy, you define recipe templates.

Following is a typical set of default recipe templates, though the precise set of default templates that a batch interface provides for a BES is vendor-specific.

```text
RECIPE[1].NAME=[PROCEDURE] 
RECIPE[1].CATEGORY=OSIBatch 
RECIPE[1].TEMPLATE=Procedure 
RECIPE[1].BATCHID=[BATCHID] 
RECIPE[1].PRODUCT=[PVAL] 
RECIPE[1].PRODUCTTRIGGER=[EVENT, value="Recipe Header"][DESCRIPT, value="Product Code"] 
RECIPE[1].PROPERTY[1].NAME=[Descript] 
RECIPE[1].PROPERTY[1].VALUE=[Pval] 
RECIPE[1].PROPERTY[1].ENGUNITS=[EU] 
RECIPE[1].PROPERTY[1].CATEGORY=Recipe Header 
RECIPE[1].PROPERTY[1].TRIGGER=[Event, value="Recipe Header"] RECIPE[1].PROPERTY[2].NAME=[Descript] 
RECIPE[1].PROPERTY[2].VALUE=[Pval] 
RECIPE[1].PROPERTY[2].CATEGORY=Formula Header 
RECIPE[1].PROPERTY[2].TRIGGER=[Event, value="Formula Header"] 

RECIPE[2].NAME=[UNITPROCEDURE] 
RECIPE[2].CATEGORY=OSIBatch 
RECIPE[2].TEMPLATE=UnitProcedure 
RECIPE[2].BATCHID=[BATCHID] 
RECIPE[2].MODULEPATH=[AREA]\[PROCESSCELL]\[UNIT] 
RECIPE[2].PRODUCT=[PVAL] 
RECIPE[2].PRODUCTTRIGGER=[EVENT, value="Recipe Header"][DESCRIPT, value="Product Code"] 

RECIPE[3].NAME=[OPERATION] 
RECIPE[3].CATEGORY=OSIBatch 
RECIPE[3].TEMPLATE=Operation 

RECIPE[4].NAME=[PHASE] 
RECIPE[4].CATEGORY=OSIBatch 
RECIPE[4].TEMPLATE=Phase 
RECIPE[4].MODULEPATH=[AREA]\[PROCESSCELL]\[UNIT]\[PHASEMODULE] 
RECIPE[5].NAME=[PHASESTATE] 
RECIPE[5].CATEGORY=OSIBatch 
RECIPE[5].TEMPLATE=PhaseState 
RECIPE[6].NAME=[PHASESTEP] 
RECIPE[6].CATEGORY=OSIBatch 
RECIPE[6].TEMPLATE=PhaseStep
```

## Translation templates

Following is a simple template that translates German source data to English for storage in the PI System.

```text
TRANSLATE: "Grundrezept" = "Procedure"
TRANSLATE: "Teilrezept" = "Unit Procedure"
TRANSLATE: "Grundoperation" = "Operation"
TRANSLATE: "Grundfunktion" = "Phase"
```

## Translation templates

Following is a simple template that translates German source data to English for storage in the PI System.

TRANSLATE: "Grundrezept" = "Procedure" TRANSLATE: "Teilrezept" = "Unit Procedure" TRANSLATE: "Grundoperation" = "Operation" TRANSLATE: "Grundfunktion" = "Phase"

<!-- Added content for ABB 800xA below -->

## DCS Link Template Settings

To define event frame linking between event frames created by different interfaces, you create dcs link templates. The WRITELINK and READLINK options on the appropriate interfaces must be configured for these templates to function. The syntax for DCS link templates is as follows:

```text
DCSTEMPLATE[<index>].<setting> = <value>
```

The `<index>` is a unique identifier used to group the settings for a particular link template. To include data from the data source, specify placeholders.

For example, if you define the following template:

```text
DCSTEMPLATE[1].Value=EF_Prefix[Pval]:1
```

...and the interface applies it to the following incoming data:

```text
[Pval]=BatchId
```

The triggering event frame is linked to the following event frame:

```text
EF_PrefixBatchId:1
```

The following headings describes the settings required to define DCS Link Templates.

### VALUE
      
(Required) Specifies the name of the event frame to be linked to by the triggering event frame. To compose the value, you can use free text plus valid placeholders.

Basic examples:

```text
DCSTemplate[1].Value = [Pval]
DCSTemplate[1].Value = [BatchID] | event: <State*> | [Descript] | val: [Pval]
```

Advanced parsing:

`DCSTemplate[1].Value = [BatchID] | event: [*,value="State*"] | [Descript] | val: [Pval]`

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
* [*,value="Exact Field"],
* [*,value="Field Mask"],
* advanced parsing

### TRIGGER
    
Specifies the event that causes the interface to generate the link. To define a trigger, specify an expression composed of a placeholder and value. When the interface detects the specified value in the placeholder, it generates the link. You can specify multiple triggers for a single link. If you specify the triggers on a single line, the link is generated only when all the conditions are met (logical AND). If you specify the trigger expressions on separate lines, the link is generated when any of the conditions is met (logical OR). 

Examples:

```text
DCSTemplate[1].Trigger = [Descript, value="WorkflowID"]
DCSTemplate[1].Trigger = [Parameter, value="State Ch*"]
DCSTemplate[1].Trigger = [Value, value="tes*"]
DCSTemplate[1].Trigger=[Event, value="State*] [Pval,value=RUNNING"]
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
* [*,value="Exact Field"],
* [*,value="Field Mask"],
* advanced parsing
