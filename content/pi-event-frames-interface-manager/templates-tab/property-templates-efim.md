---
uid: BIF_PropertyTemplatesEFIM
---

<!-- Mark Bishop 6/8/21: Modified batch framework topic. -->

# Property templates

Property templates enable you to configure how data from the data source is written to event frame attributes or batch database properties. Each interface provides a set of default properties, which contain commonly-desired data. To add these properties, right-click the **Property Templates** node and choose **Add Default Templates**.

## Configuration

### Index

Assigns a unique numeric identifier for the template. 

### Name
    
Specifies how the property is named. You can use placeholders to include values emitted by the data source. By default, properties reside under a parent recipe property. To specify a location in the hierarchy where you want the property to reside, define the name as a path, delimited using backslashes. For example, to specify that all properties generated using this template are located under a parent property named "Materials" plus the contents of the **Event** field, specify the name as follows: `Materials\[Event]`. To create the property at the root level, precede the name with a dollar sign: `$\[Event]`. 

### Value
    
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

### UOM
    
Unit of measure to be used to store value, if different from unit provided by data source. 

<!-- Mark Bishop 6/8/21: Added property template placeholders -->

### Property template placeholders
    
See <xref:TemplatePlaceholders> for the complete list of available placeholders.

## Advanced features

### Descriptor
    
Populates the tag's Descriptor field. 

### Engineering units
    
Unit of measurement. 

### Category
    
Specifies the PI AF category to be associated with the value. 
