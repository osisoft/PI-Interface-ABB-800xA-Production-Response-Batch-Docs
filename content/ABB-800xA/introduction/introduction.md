---
uid: Introduction
---

# Introduction to PI Interface for ABB 800xA Production Response Batch

The PI Interface for ABB 800xA Production Response Batch, which is based on a common batch interface framework discussed in this user guide, uses event streaming technology to collect ABB system data from ABB API.

PI interfaces for batch and manufacturing execution systems are scan-based interfaces that populate the PI AF database (with event frames and elements) based on events and data read from a data source. The interfaces can be configured to create and update PI tags based on the data received. The interface cannot update the batch data source.
    
>To use event frames, your PI batch interface must be version 3.x or higher.

Unlike other OSIsoft interfaces, batch-related interfaces do not use PI buffering. Batch data is persistent in the data source and not in danger of being lost. If the interface loses its connection to the PI Data server, it continues to collect data from the data source, transmitting it to the server when the connection is reestablished. Similarly, you need not configure failover for batch interfaces. If for any reason the interface is unable to collect data, the data remains available in the database or event files and you can use recovery mode to fill in any data that was missed during the time the interface was down.
    
>These interfaces are designed for recipes that constrain a unit to run only one unit procedure at a time.

Two different models are used to describe batch processes. The equipment model describes the physical equipment necessary to create a batch while the recipe model describes the procedures that are performed during the execution of a recipe. There is no intrinsic or direct relationship between the models. With the exception of arbitration events, journal files contain only recipe model event information.

The S88 process model is composed of the following hierarchy:

* Procedure (recipe)
* Unit procedures
* Operations
* Phases
* Phase steps
* Phase states

The physical model is composed of the following equipment-oriented hierarchy:

* Enterprise
* Site
* Area
* Process cell
* Unit
* Equipment module
* Control module

Unit procedures from the data source are mapped to PI UnitBatches. Only a single unit procedure can be active in a unit at any given time, which restricts the configuration of recipes that can be run by the batch execution system if batch data is to be captured by the interface in a reliable and meaningful way. By contrast, event frames support parallel unit procedures natively. You can configure interfaces to create PI tags and properties by defining templates, which specify the events that trigger creation, configure how the property or tag is named, and define the data to be stored.
