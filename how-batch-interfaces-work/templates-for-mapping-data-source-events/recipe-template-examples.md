---
uid: BIF_RecipeTemplateExamples
---

# Recipe template examples

Configure the batch name as the concatenation of the procedure and unique ID fields from the data source, and name operations by concatenating the parent unit procedure name with the operation name:

```text
Recipe[1].Name = [Procedure]_[UniqueID]
Recipe[3].Name = [UnitProcedure]_[Operation]
```

Assign the PI AF category "CAT_UNITBATCH" to all unit procedures. Note that, if the specified category has not been defined in PI AF, the interface creates it.

```text
Recipe[2].Category = CAT_UNITBATCH
```

Dynamically assign categories based incoming data:

```text
Recipe[1].Category[1].Name = PROC_A
Recipe[1].Category[1].Trigger = [Procedure, value="DVProc:1-*"]
Recipe[1].Category[2].Name = [Pval]
Recipe[1].Category[2].Trigger = [Descript, value="Product Code"]
```

When creating event frames for unit procedures (level 2), use the corresponding template:

```text
Recipe[2].Template = OSI_UnitProcedure
```

Dynamically assign templates based incoming data:

```text
Recipe Template Example 5:
Recipe[2].Template[1].Name = UP_A
Recipe[2].Template[1].Trigger = [UnitProcedure, value="UProc:1-*"]
Recipe[2].Template[2].Name = UP_B
Recipe[2].Template[2].Trigger = [UnitProcedure, value="UProc:2-*"]
```
