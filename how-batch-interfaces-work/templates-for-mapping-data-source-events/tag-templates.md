---
uid: BIF_TagTemplatesBatch
---

# Tag templates

This section details the procedure for configuring tag templates. The tables in steps 7 and 8 define specific tag template settings and configurations to ensure that tag templates capture updates to PI Batch Database.

1. To create or update PI tags when specified events are read, configure tag templates.

2. To create or update PI tags based on alarms read from an Emerson DeltaV Event Chronicle (alarms & events) data source, configure alarm tag templates.

3. To define tag templates using PI Event Frame Interface Manager, go to the **Templates** page and click the **Tag** tab.

4. To configure the name of the tag to be created or updated, specify the **Name** field. To assign tag names based on incoming data, use placeholders.

    For example, to track phase module report events on a per-unit basis, you might configure the name as follows:

    ```text
    [Unit] [phasemodule] Report
    ```

    With the preceding template, when the interface reads a report event for the NORTON phase module on unit XUNIT_52003, it replaces the placeholders with data from the specified fields and creates or updates a PI tag with the following name:

    ```text
    XUNIT_52003 NORTON Report
    ```

    If the name structure contains placeholders, the tag template is triggered only if all the corresponding fields from the incoming event contain data (that is, are not blank).

    Different templates can update the same PI tag, if the templates' name structure resolves to the same tag. This capability enables you to write different values to the tag depending on the nature of the triggering event. For example, a value of 1 can be written to the tag when a unit procedure starts and a value of 0 can be written to the same tag when the unit procedure ends.

5. To specify the data to be written to the tag, configure the **Value** field. To include data read from the data source in the tag value, use placeholders.

    For example, to simply record the incoming value without transforming it, specify the [PVAL] placeholder. A more complex example: to configure a value that concatenates phase module, event, description, incoming value and engineering units, specify the following:

    ```text
    [PHASEMODULE].[EVENT].[DESCRIPT]: [PVAL] [EU]
    ```

    The preceding expression generates data like the following:

    ```text
    CHARGE_DIW.Recipe Value.CPP_HIGH_LIMIT: 2535 kg
    ```

    Unlike placeholders in tag names, value placeholders can be replaced with empty fields from the incoming event, unless you use advanced field parsing to configure the value.
    
6. To update a tag when a particular event is read from the data source, specify the EVENT keyword in the **Name** field, as follows:

    ```text
    [EVENT, VALUE="event_text"]
    ```

    This approach enables you to write different values to the tag depending on the text in the EVENT column.

    If you require a more refined approach, specify the incoming data that causes the template to be evaluated by configuring one or more triggers on the **Trigger** tab of the tag template.

    To configure the template to handle multiple different events, specify separate triggers ("OR" logic). To ensure that the template is triggered only when a set of multiple conditions are all detected ("AND" logic), specify a single trigger containing all the conditions. For example, to trigger the template only for system message events that are phase logic failures, specify the trigger as follows:

    ```text
    [EVENT, value="System Message"] [DESCRIPT, value="Phase Logic Failure"]
    ```

    To ignore specified incoming values, use "!=" (not equal) . For example, to ignore undefined values, specify the following expression:

    ```text
    [PVAL, VALUE!="UNDEFINED"]
    ```

    You can use wildcards to specify pattern-matching expressions in triggers.

7. To configure the tag template settings, specify settings as described in the following table:

    | Setting | Description |
    |--|--|
    | **NAME** | (Required) Name of PI tag to be created or updated. |
    | **VALUE** | (Required) Value to be assigned to PI tag (text) |
    | **TRIGGER** | Event text from data source (can be specified using wildcards) |
    | **TYPE** | String/integer/float/auto. "Auto" directs the interface to automatically detect the data type. |
    | **UNITALIAS** | Configure how unit alias (AF: PI point reference) is created. By default, the alias is created in the unit. To override the default, specify the path where you want the alias created. For example:<br><br>`UNITALIAS = \Building1\Unit2|[PHASE]`<br><br>The alias is created under the Unit2 module, named using the value of the [PHASE] column.<br><br>**Note:** All batch interfaces support unit- and phase-level equipment aliases. Some interface support creation of equipment aliases at all levels of the batch hierarchy. For details, refer to the interface-specific section of this guide. |
    | **PHASEALIAS** | Configure how the phase alias is created. By default, the alias is created in the phase module. To override the default, specify the path where you want the alias created. |
    | **DESCRIPTOR** | Value for PI point descriptor attribute. |
    | **ENGUNITS** | Engineering units |
    | **TRANSLATE** | To enable translation, set to TRUE (default: FALSE) |
    | **ANNOTATION** | Simple annotation to be written to the tag when the interface updates it. |
    | **ANNOTATION2** | Structured annotation to be written to the tag when the interface updates it. For details about structured annotations, refer to the PI Data Archive System Management Guide. |

8. To configure tag templates that catch events raised by the interface when it updates the PI Batch Database, specify the following placeholders in the TRIGGER setting of the tag template:

    | Placeholder | Values | Description |
    |--|--|--|
    | **EVENT** | **PIEVENT** | Specify [EVENT, value="PIEVENT"] |
    | **DESCRIPT** | **BATCH**<br>**UNITBATCH**<br>**OPERATION**<br>**PHASE**<br>**PHASESTATE**<br>**PHASESTEP** | Specify the batch level you want to trigger on. For example:<br><br>[DESCRIPT, value="UNITBATCH"]<br>[DESCRIPT, value="PHASE"] |
    | **PVAL** | **START**<br>**END** | Specifies whether to catch the start or ending event of the specified level:<br><br>[PVAL, value="START"]<br>[PVAL, value="END"] |
    
    For example, to detect the start of a batch, specify the following expression:

    ```text
    [EVENT, VALUE="PIEVENT"][DESCRIPT, VALUE="BATCH"][PVAL, VALUE="START"]
    ```

    The following placeholders are supported when the triggering expression contains [Parameter, value="PIEVENT"].

    | Placeholder | Batch Database | Event Frames |
    |--|--|--|
    | [BATCHID] | PIBatch and PIUnitBatch: BatchID property. | For a top-level event frame, "Name" property. For second-level event frame, "BatchID" attribute |
    | [PROCEDURE] | PIBatch "Recipe" property | Event frame "Recipe" attribute |
    | [UNITPROCEDURE] | PIUnitBatch "Procedure" property | Event frame "Name" property |
    | [OPERATION] | PISubBatch "Name" property | Event frame "Name" property |
    | [PHASE] | Level 4 PISubBatch "Name" property | Event frame "Name" property |
    | [PHASESTATE] | Level 5 PISubBatch "Name" property | Event frame "Name" property |
    | [PHASESTEP] | Level 6 PISubBatch "Name" property | Event frame "Name" property |
    | [UNIT] | PIUnit "Name" property | Event frame "Name" property |
    | [PHASEMODULE] | Phase module "Name" property | Event frame "Name" property |
