---
uid: BIF_Introduction
---

# Introduction to [!include[interface](../includes/product-long.md)] [!include[interface](../includes/product-version.md)]

<!-- Add customized content between comments for the interace you're writing for -->



<!-- end comment-->

<!-- Content below applies to all interfaces. -->

Two different models are used to describe batch processes: 

1. The **equipment model** describes the physical equipment necessary to create a batch. 

2. The **recipe model** describes the procedures that are performed during the execution of a recipe. 

There is no intrinsic or direct relationship between the models. With the exception of arbitration events, journal files contain only recipe model event information. 

The interface is compliant with the ISA S88.01 standard and uses the S88 process model, which is composed of the following hierarchy: 

* Procedure (recipe) 
* Unit procedures 
* Operations 
* Phases 
* Phase steps 
* Phase states 

**Note:** According to the ISA S88.01 standard, procedures and unit procedures are optional. A recipe can be composed solely of operations and phases. The PI Batch Database does not use a strict S88 approach to describe or record batch data.

The physical model is composed of the following equipment-oriented hierarchy:

* Enterprise 
* Site 
* Area 
* Process cell 
* Unit 
* Equipment module 
* Control module 

Unit procedures from the data source are mapped to PIUnitBatches. Only a single unit procedure can be active in a unit at any given time, which restricts the configuration of recipes that can be run by the batch execution system if batch data is to be captured by the interface in a reliable and meaningful way. By contrast, event frames support parallel unit procedures natively. 

You can configure the interface to create PI points and properties by defining templates, which specify the events that trigger creation, configure how the property or tag is named, and define the data to be stored. 