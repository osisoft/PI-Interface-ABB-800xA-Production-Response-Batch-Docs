---
uid: BIF_AlarmTagTemplates
---

# Alarm tag templates

Alarm tag templates allow you to configure the event notifications you will receive.

## Configuration

### Index

Assigns a unique numeric identifier for the template.

### Name

Specifies how the alarm tag is named.

Click the **Name** field to activate the **Add Placeholder** button. Click the button to open the **Build a Placeholder** window. There you can select and add a placeholder and select from the following Advanced parsing features:

* **Add value**: Select to add and specify placeholder values. Click **Add** to save your changes.

* **Add substring parsing**: Select and specify substring values. Click **Add** to save your changes.

    * Select **Left bound** and either **LBE** or **LBI** from the dropdown menu to define the left boundary of the substring.
    * Select **Right bound** and either **RBE** or **RBI** to define the right boundary of the substring.
    * Select **Delimiter** then provide a name and a count to narrow the resulting substring.

### Value

Specifies the value to be recorded. As with the **Name** field, click the **Value** field to activate the **Add Placeholder** button. You can edit placeholders to include values from the data emitted by the data source.

### Data type

Specifies the PI data type of the value from the following options:

* String
* Integer
* Float
* Auto
* Float or string

### Translate

Click the checkbox to activate the **Translate** button, which you can click to open the **Translate** window. There you can add and remove English Text and Foreign Text.

## Advanced features

### Descriptor

Populates the tag's Descriptor field.

### Engineering units

Unit of measurement.

### Alias

Use the drop down menu to select from the following:

* **Default**: Defaults to alias name and filepath.

* **Custom alias name**: Provide a custom alias using one of the following format examples:

  * Tag(#)alias = ABC\def |test[module]
  
  * Tag(#)alias = $\[Area] |[module] ALARM alias

* **Disable alias creation**: No alias is created.

### Annotation

Use the field provided to annotate the alarm tag.

You have the option of selecting the **Use a NameValues collection for annotation** or **Remove annotation from tag value**.
