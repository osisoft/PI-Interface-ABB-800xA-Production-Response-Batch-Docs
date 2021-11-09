---
uid: BIF_Overview
---

# Batch interface overview

<!-- Framework topic. Usually requires no edits. -->

[!include[interface](../includes/product-long.md)] is classified as a PI interface for Batch Execution Systems (BES) and Manufacturing Execution Systems (MES), which are based on a common framework. 

**Note:** If you record batch process data directly to PI tags and do not use a BES, you can generate batch data from PI tag data using the PiBaGen or PIEFGEN utilities. For details, refer to the manuals for these applications. For details, refer to the manuals for these applications.

PI batch interfaces are scan-based interfaces that populate either

* PI AF database (with event frames and elements) or 
* PI Batch Database and PI Module Database (with batches and modules) based on events and data read from a data source. The interfaces can be configured to create and update PI points based on the data received. The interface cannot update the batch data source.               

**Note:** To use event frames, your PI batch interface must be version 3.x or higher.                   

Batch interfaces can read data from multiple data sources, which enables the PI server to handle scenarios in which different overlapping batch recipes can access the same unit in different stages of the production cycle. By acquiring data for the same time frame from multiple sources and collating it into a single time-ordered sequence, a single interface instance can capture the complete history of the batch process.

Unlike other OSIsoft interfaces, batch-related interfaces do not use PI buffering. Batch data is persistent in the data source and not in danger of being lost. If connection to the PI server is lost, the interface continues to collect data from the data source, transmitting it to the PI server when the connection is reestablished. If for any reason the interface is unable to collect data, the data remains available in the database or event files and you can use recovery mode to fill in any data that was missed during the time the interface was down.

**Note:**  These interfaces are designed for recipes that constrain a unit to run only one unit procedure at a time.

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