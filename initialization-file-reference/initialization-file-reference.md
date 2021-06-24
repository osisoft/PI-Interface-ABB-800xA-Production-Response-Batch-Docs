---
uid: BIF_InitializationFileReference
---

# Initialization file reference

<!-- Topic requires customization for specific interface -->

The initialization (.ini) file stores configuration information for an interface instance. This file is generated and updated by the PI Event Frame Interface Manager configuration tool. To enable you to control access to these files, initialization files are stored under the ProgramData folder. (Note that, prior to release 4.x, initialization files were stored in the interface installation directory.)

**Note:** To ensure a correctly configured .ini file, use the PI Event Frame Interface Manager configuration tool. Do not edit the .ini file manually.

The information in this appendix is intended for troubleshooting purposes, to enable you to understand the contents of the .ini file.

The .ini file is divided into the following sections:

* **COMMAND LINE PARAMETERS:** Basic interface settings.
* **SIMPLE SWITCHES:** Connection settings.
* **SOURCE TEMPLATE:** Specifies the settings required to connect to the data source, and events to be skipped (filtered)
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

Following are some simple examples of data source templates.

Single DeltaV Batch Historian:

```text
Source[1].sqlserver = deltav10 Source[1].database = DVHisDB
```

DeltaV Batch Historian plus Alarms and Events:

```text
Source[1].sqlserver = deltav10 Source[1].database = DVHisDB Source[2].sqlserver = deltav10\DELTAV_CHRONICLE Source[2].database = Ejournal Source[2].isAE = true
```

### Data source template parameters

The following headings describe the parameters for data source templates.

#### `cursor= client | server` 

Optional for SQL data source. Available in DeltaV 9.3+.

* Client (default): The interface retrieves complete dataset prior to processing. High memory consumption on interface node.
* Server: The interface requests and processes one dataset record at a time. Reduces interface node memory consumption.

#### `evtdir=<path>`

Required for event file data sources, specifies the folder that contains the event files. 

Example:

```text
Source[1].evtdir = D:\TEST\RELEASE\test_1
``` 

#### `excludestates=<list>`

(Optional) Specifies a comma-separated list of phase states to ignore. Not case-sensitive. You can use wildcards for matching. 

Examples:

```text
excludestates=COMPLETED,AB*ING,IDLING, COMPLE*
```

#### `isAE=true`

Indicates that the data source is a DeltaV Alarms and Events server.

#### `opcnode=<node name or IP address>`

Required for OPC alarms and events data source. Available in DeltaV 10.3 and higher. Specifies the host of the DeltaV OPCAE server is installed. If used with DeltaV SQL server, must be defined for the same source. 

Example:

```text
Source[1].sqlserver = deltav10
Source[1].sqldatabase = DVHisDB
Source[1].opcnode = deltav10
Source[1].opcserver = DeltaV.OPCEventServer.1
```

#### `opcserver=<server name>`

Optional for OPC alarms and events data source. Specifies the name of the alarms and events server, if you are not using the default server.

#### `skipphases=<list>`

(Optional) Specifies a comma-separated list of phases to ignore. Not case-sensitive. You can use wildcards for matching. The interface checks the list against the [Phase] field (batch recipe) or [PhaseModule] field (equipment). 

Examples:

```text
skipphases=phase_1, ph*2,ph_test*, ph*ort*
```

#### `skiprecipes=<list>`

(Optional) Specifies a comma-separated list of recipes to ignore. Not case-sensitive. You can use wildcards for matching. The interface checks the list against the corresponding event field, depending on recipe type, as follows:

```text
skiprecipes=recipe_1, rec*2,PRC_PAINT*, UP_TEST:2
```

#### `skipunits=<list>`

(Optional) Specifies a comma-separated list of units to ignore. Not case-sensitive. You can use wildcards for matching. The interface checks the list against the corresponding [Unit] field. 

Example:

```text
skipunits = unit_1, u*2
```

#### `sqlserver=<node name or IP address>`

Required for SQL Server data source. Specifies the host where SQL Server is running. Available in DeltaV 9.3+.

#### `sqldatabase=<database name>`

Optional for SQL Server data source. Specifies the name of the database, if you are not using the default database. (DVHisDB).

#### `sqlpswd=<password>` 

For explicit login to SQL Server, password for user specified in sqluser setting.

#### `sqluser=<user name>` 

User name for explicit login to SQL Server. By default the interface uses Windows authentication to connect to SQL Server.

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

The following headings describes the settings required to define property templates.

#### NAME 

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

#### VALUE 

(Required) Specifies the value to be stored in the property. To compose the value, you can use free text plus valid placeholders.

Basic example:

```text
Property[1].Value = [BatchID] | event: <State*> | [Descript] | val: [Pval] 
```

Advanced parsing:

```text
Property[1].Value = [BatchID] | event: [*,value="State*"] | [Descript] | val: [Pval]
```

**Note:** For SQL dta sources with the "Use original batch event view" option enabled (/UOBEV), you cannot use the [PVAL] or [EU] placeholders. To obtain this data you must parse it from the [DESCRIPT] placeholder.

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

#### TRIGGER 

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

#### TRANSLATE 

To specify that the value is to be translated according to the translation map you define set this setting to TRUE.

**Valid Placeholders**

* TRUE 
* FALSE

#### TYPE

Specifies the data type for the value. To configure the interface to evaluate the data and assign the data type accordingly, specify **AUTO**.

**Valid Placeholders**

* STRING
* FLOAT
* INTEGER
* AUTO

#### CATEGORY 

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

#### UOM or ENGUNITS or EU

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

### Tag template settings

The following table lists valid settings for tag templates. The timestamp for tag events is taken from the triggering event.

#### ANNOTATION 

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

#### ANNOTATION2 

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

#### DESCRIPTOR 

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

#### EU 

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

#### NAME

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
 
#### PHASEALIAS

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

#### TRIGGER

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

#### TRANSLATE 

To specify that tag settings are to be translated according to the translation map you define, set this setting to TRUE.

**Valid Placeholders**

* TRUE
* FALSE

#### TYPE

Specifies the data type for the tag. To configure the interface to evaluate the data and assign the data type accordingly, specify AUTO.

**Valid Placeholders**

* STRING
* FLOAT
* INTEGER
* AUTO

#### UNITALIAS 

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

#### VALUE

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

## Recipe Templates

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

## Translation Templates

Following is a simple template that translates German source data to English for storage in the PI System.

```text
TRANSLATE: "Grundrezept" = "Procedure"
TRANSLATE: "Teilrezept" = "Unit Procedure"
TRANSLATE: "Grundoperation" = "Operation"
TRANSLATE: "Grundfunktion" = "Phase"
```
