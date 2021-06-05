---
uid: TemplatesTab1
---

# Templates tab

To override the default way that batch data is stored in the PI System, you define templates. Attribute templates enable you to record batch data in PI AF event frame attributes. To specify how the data is to be formatted, you use placeholders. For example, if you specify the following template (note the placeholders in square brackets):

```
Sample [Time] | [Descript]-[BatchID]:[Event]__pvalue:[Pval][EU]
```
... resulting data is formatted like the following example:

```
Sample 2007/12/11 05:19:12:184 | Product Code:Recipe Header__pvalue:UNDEFINED
```

To enable you to precisely extract the required data from incoming fields, batch interfaces support advanced parsing features. For detailed information about placeholders and advanced parsing, refer to the user guide for your batch interface.
