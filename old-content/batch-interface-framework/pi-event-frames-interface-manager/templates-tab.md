---
uid: BIF_TemplatesTab
---


# Templates tab

<!-- Customized for ABB 800xA. -->

Templates map data from the data source to PI tags, batches and event frames. When defining templates, you specify the data to be written and the events that trigger the update. To define templates using PI Event Frame Interface Manager, go to the Templates page and navigate to the desired type of template. You can configure templates that map the source data to string, integer or float data types. For each type of template, you specify triggers, which are conditions that active the template.

You can define the following types of templates:

* **Tag:** Creates and updates PI tags, specifying how they are named and what data is written to them.
* **Property:** Maps data to batch properties in the PI Batch Database or event frame attributes in PI AF.
* **Recipe:** Defines the information stored and the naming convention used at each level in the generated batch hierarchy.

<!-- Mark Bishop 6/8/21: Alarm tag does not apply to ABB 800xA. 

* **Alarm tag:** Writes data to a PI tag when the data source raises an alarm.

-->

The following sections provide details about the specific types of templates.
