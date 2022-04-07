---
uid: BIF_TagTemplatesEFIM
---

# Tag templates

Tag templates create and update PI tags when events are read from the data source. If you define one or more triggers, the target PI tag is updated only when the specified events occur. If you do not define any triggers, every event from the data source triggers an update of the target PI tag.

Tag aliases enable you to associate PI tags with equipment assets (PI units or AF elements). All batch interfaces support the creation of aliases at the unit batch and phase level. In addition, some batch interfaces permit you to define aliases at any level of the batch hierarchy by providing level-specific placeholders. For details, refer to the interface-specific section in this guide.

## Tag configuration

| Attribute | Definition |
| --------- | ---------- |
| Index | Specify a unique numeric identifier for the entry. |
| Name |  Configures how the tag is named. To include data from the data source, use placeholders. |
| Value | The value to be written to the PI tag. To include data from the data source, use placeholders. |
| Type |  The data type to be used to write the value to the tag. Note that if the incoming value is incompatible with the tag type, the event is not processed, and an error is logged. |
| Translate | Maps text from the data source to the text that you want to record in the PI System. |

## Advanced features (attributes)

| Attribute | Purpose |
| --------- | ------- |
| Descriptor | Populates the descriptor field for the target PI tag. |
| Engineering units | The engineering units for the data. 
Unit Alias | Specifies an alias to be recorded under the Aliases node in the corresponding PIUnit or AF element. |
| Phase Alias | Specifies an alias to be recorded under the Phases > Aliases node in the corresponding PIUnit or element. |
| Annotation | Specifies the annotation to be associated with the event. The result is stored in a PI tag as a string. |
| Use the NamedValues collection for annotations | Store annotations in a PI tag as a name-value collection. The name is derived from the event sent by the data source. |
| Remove annotations from tag values | Store values without annotations. |
