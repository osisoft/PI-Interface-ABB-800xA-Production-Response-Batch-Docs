---
uid: BIF_RecipeTemplatesEFIM
---

# Recipe templates

<!-- Topic requires customization for specific interface -->

Recipe templates enable you to configure the names that are assigned and the data that is stored at each level of the batch hierarchy. A set of default recipe templates are is included with each batch interface. To display and override the default recipe templates, right-click the **Recipe Templates** node and choose **Add Default Templates**. The settings for recipe templates are as follows.

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

### Name

Defines the naming convention used by the interface to assign names to batch events. For event frames, this template modifies the Recipe AF attribute. For the Batch database, this template modifies the PIBatch name.

For example: abc_[Procedure] If the incoming event's [Procedure] field contains "Test", the resulting procedure **Recipe** field is "abc_Test".

## Advanced features

### Batch ID

Configures the batch ID of the particular recipe object, overriding the incoming (default) batch ID. If you override the batch ID for the procedure, the batch ID is propagated to the child unit batches Batch ID field. For event frames, this template modifies the event frame name.
        
**Note:** If you use a recipe template to set the batch ID, the recipe template overrides any batch ID mask you might have configured to enable merging of batches.

### Module/Element Path

Specifies the location in the PI module or AF element hierarchy where the unit or phase module resides. Valid for unit procedure (level 2) and phase (level 4). 

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
