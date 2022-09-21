---
uid: BIF_RecipeTemplatesEFIM
---

<!-- Mark Bishop 6/8/21: Modified batch framework topic. -->

# Recipe templates

<!-- Topic requires customization for specific interface -->

Recipe templates enable you to configure the names that are assigned and the data that is stored at each level of the batch hierarchy. A set of default recipe templates is included with each batch interface. To display and override the default recipe templates, right-click the **Recipe Templates** node and choose **Add Default Templates**. The settings for recipe templates are as follows.

## Configuration

### Index

Specifies the level in recipe hierarchy as follows:

| Level | Index | PI object | Default |
| ----- | ----- | --------- | ------- |
| Procedure | 1 | PIBatch Recipe | Recipe[1].Name=[Procedure] |
| Unit Procedure | 2 | PIUnitBatch Procedure | Recipe[2].Name = [UnitProcedure] |
| Operation | 3 | PISubBatch Name field | Recipe[3].Name=[Operation] |
| Phase | 4 | PISubBatch Name field | Recipe[4].Name=[Phase] |
|Phase State | 5 | PISubBatch Name field | Recipe[5].Name=[PhaseState] |
| Phase Step | 6 | PISubBatch Name field | Recipe[6].Name=[PhaseStep] |

**Note:** Phase State (PHASESTATE) and Phase Step (PHASESTEP) levels only exist in the recipe hierarchy after enabling the BATCHRCP interface (BATCHRCP = true).

### Name

Defines the naming convention used by the interface to assign names to batch events. For event frames, this template modifies the Recipe AF attribute. For the Batch database, this template modifies the PIBatch name.

For example: abc_[Procedure] If the incoming event's [Procedure] field contains "Test", the resulting procedure **Recipe** field is "abc_Test".

### Value

**Note**: The **Value**, **Create property**, **Data type**, and **Translate** options are only available for recipe template properties.
    
Specifies the value to be recorded. Use placeholders to include values from the data emitted by the data source. 

### Create property
    
Specifies the level at which the property is to be created. Options are as follows:

* **At recipe level**: By default, properties are created at the recipe level corresponding to the level in the data source from which the data was read.

* **Under root node**: Create properties at the top level of the batch or event frame hierarchy, regardless of the level at which they originated.

* **Under UniqueID node**: (Batch database only, not event frames) Create properties under the batch's UniqueID node.

### Data type
    
PI data type of the value. Note that if the incoming value is incompatible with the specified type, the event is not processed, and an error is logged. 

### Translate

Maps text from the data source to the text that you want to record in the PI System. 
    
Specifies the value to be recorded. Use placeholders to include values from the data emitted by the data source. 

## Advanced features

### Batch ID

Configures the batch ID of the particular recipe object, overriding the incoming (default) batch ID. If you override the batch ID for the procedure, the batch ID is propagated to the child unit batches Batch ID field. For event frames, this template modifies the event frame name.

In the Procedure level recipe template, the interface uses the Batch ID field for the name of the Event Frame if it is the top level of the batch hierarchy. If the Batch ID field is empty, an error is returned during recipe template processing. If you are using a truncated Batch ID and the Batch ID field is not empty, the interface uses the Batch ID that matches the mask provided by the BIDM for the Batch ID. BIDM only shows noticeable difference in Event Frames that use the Batch ID field for their names.

In the Unit Procedure level recipe template, the interface uses the Name field for the name of the Event Frame based on the Batch Recipe (for example, level is *s88_UnitBatch*). The Batch ID field is an attribute/property in the Event Frame.

In the Operation level recipe template and all other sub batches, the interface uses the Name field for the name of the Event Frame. The Event Frame does not store the Batch ID field.
        
**Note:** If you use a recipe template to set the batch ID, the recipe template overrides any batch ID mask you might have configured to enable merging of batches.

### Module/Element Path

Specifies the location in the PI module or AF element hierarchy where the unit or phase module resides. Valid for PIBatches (level 1), unit procedure (level 2) and phase (level 4) and uses configuration. 

### Product

Specifies the product of the particular recipe object. Supports the procedure and unit procedure [Product] fields, which must be present in the source event that creates the batch. If a product trigger is not defined, this template is populated based on the data in the event that creates the particular Recipe object. 

### Product Trigger

Populates the [Product] field of the particular recipe object after the object is created, which is useful if the product is defined in a separate event.

For example: `[Parameter, Value="Recipe Header"] [Descript, value="Product Name"]`.

### Event Frame Template

(Event frames only) Specifies the AF template to be used to create event frames for this recipe. 

### Category

(Event frames only) Specifies the AF category to be applied to the event frame. 

### Merge same named objects under parent

Combines identically named child objects. 

<!-- Mark Bishop 6/8/21: Added content for ABB 800xA. -->

## Recipe template placeholders

See <xref:TemplatePlaceholders> for the complete list of available placeholders.
