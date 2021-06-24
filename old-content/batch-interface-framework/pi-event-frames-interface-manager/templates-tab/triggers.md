---
uid: BIF_Triggers
---

# Triggers

<!-- Topic requires customization for specific interface -->

To specify the events that initiate updates to tags or properties, you define triggers. You can define triggers for events read from the data source and for batch-related events raised by the PI System itself (PI Events). To define triggers using PI Event Frame Interface Manager, go to the Templates page, navigate to the desired tag or property template, and click the Triggers tab.

If you omit triggers, the target is updated by every event. If you specify multiple conditions in a single trigger, data is written only when all conditions are met (logical AND). If you define multiple triggers, data is written when any one of the conditions is met (logical OR).

In the following example, the template is triggered when the PI System records the start of a batch: `[Event,value="PIEVENT"] [Descript, value="BATCH"] [Pval, value="START"]`
