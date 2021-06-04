---
uid: DefineAttributeTemplates
---

# Define attribute templates

To define attribute templates using the PI Event Frames Interface Manager:

1. 	On the **Templates** tab, right-click **Attribute Templates** and choose **Add**. The Configuration pane displays.
2. 	On the **Configuration** pane, enter the following settings:
    * **Index:** Assigns a unique numeric index for the template.
    * **Name:** Specifies how the target attribute is named. To use incoming data from the data source to define how the attribute or property is to be named, click Add Placeholder… Within each hierarchy, property names must be unique. By default, properties are named Event_1, Event_2, and so on.
    * **Value:** Specifies the value to be recorded. Use placeholders to derive values from the data emitted by the data source.
    * **Data type:** PI data type of the value.
    * **Translate:** If required, specifies how any English language values are to be translated before being stored in the PI System.
    * **UOM:** (AF only) Unit of measure to be used to store value, if different from unit provided by data source.

## Advanced Features

* **Description:** (AF only) Populates the attribute's Description field.
* **Engineering units:** Unit of measurement.
* **Category:** Specifies the PI AF category to be assigned to the attribute. 