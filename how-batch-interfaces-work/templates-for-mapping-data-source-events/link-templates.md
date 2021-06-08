---
uid: BIF_LinkTemplatesBatch
---

# Link templates

DCS Link Templates associate event frames from one interface to another. To create links, you define link templates on the **Templates** page of the PI Event Frame Interface Manager. The link templates specify events that contain link data and the naming of the destination event frame. Placeholders, wildcards and advanced parsing features enable you to extract precisely the desired data from the events that the interface reads from the data source.

Triggers on the template define the events with linking information and the value specifies the name of the destination batch level event frame.
To define a link template on the **Templates** page of the PI Event Frame Interface Manager, configure the following settings:

| Setting | Description |
| ------- | ----------- |
| Value | The name of the destination batch level event frame. |
| Trigger | The event that triggers the generation of the property. Updates can be triggered by the data source or by PI events such as the start or end of a recipe level. |

To link an event frame that has an event where `Descript` is `WorkflowID` to a batch level event frame whose name is held in `Pval` in the same event, configure the template with the following settings:

| Setting | Set to |
| ------- | ------ |
| Value | [Pval] |
| Trigger | [Descript, value="WorkflowID"] |
