---
uid: BIF_Recipetemplates
---

# Recipe templates

To define the data generated for each level of the batch hierarchy, you define recipe templates.

Following is a typical set of default recipe templates, though the precise set of default templates that a batch interface provides for a BES is vendor-specific.

```text
RECIPE[1].NAME=[PROCEDURE] 
RECIPE[1].CATEGORY=OSIBatch 
RECIPE[1].TEMPLATE=Procedure 
RECIPE[1].BATCHID=[BATCHID] 
RECIPE[1].PRODUCT=[PVAL] 
RECIPE[1].PRODUCTTRIGGER=[EVENT, value="Recipe Header"][DESCRIPT, value="Product Code"] 
RECIPE[1].PROPERTY[1].NAME=[Descript] 
RECIPE[1].PROPERTY[1].VALUE=[Pval] 
RECIPE[1].PROPERTY[1].ENGUNITS=[EU] 
RECIPE[1].PROPERTY[1].CATEGORY=Recipe Header 
RECIPE[1].PROPERTY[1].TRIGGER=[Event, value="Recipe Header"] RECIPE[1].PROPERTY[2].NAME=[Descript] 
RECIPE[1].PROPERTY[2].VALUE=[Pval] 
RECIPE[1].PROPERTY[2].CATEGORY=Formula Header 
RECIPE[1].PROPERTY[2].TRIGGER=[Event, value="Formula Header"] 

RECIPE[2].NAME=[UNITPROCEDURE] 
RECIPE[2].CATEGORY=OSIBatch 
RECIPE[2].TEMPLATE=UnitProcedure 
RECIPE[2].BATCHID=[BATCHID] 
RECIPE[2].MODULEPATH=[AREA]\[PROCESSCELL]\[UNIT] 
RECIPE[2].PRODUCT=[PVAL] 
RECIPE[2].PRODUCTTRIGGER=[EVENT, value="Recipe Header"][DESCRIPT, value="Product Code"] 

RECIPE[3].NAME=[OPERATION] 
RECIPE[3].CATEGORY=OSIBatch 
RECIPE[3].TEMPLATE=Operation 

RECIPE[4].NAME=[PHASE] 
RECIPE[4].CATEGORY=OSIBatch 
RECIPE[4].TEMPLATE=Phase 
RECIPE[4].MODULEPATH=[AREA]\[PROCESSCELL]\[UNIT]\[PHASEMODULE] 
RECIPE[5].NAME=[PHASESTATE] 
RECIPE[5].CATEGORY=OSIBatch 
RECIPE[5].TEMPLATE=PhaseState 
RECIPE[6].NAME=[PHASESTEP] 
RECIPE[6].CATEGORY=OSIBatch 
RECIPE[6].TEMPLATE=PhaseStep
```


