---
uid: BIF_ThePIBatchDatabase
---

# The PI Batch Database

The PI Module and Batch Databases are used to organize and store batch data. Each object in the PI Batch Database represents a specific level of the S88 Recipe Model. To represent recipes, unit procedures, operations, phases, phase states and phase steps, the interface creates PIBatches, PIUnitBatches and a hierarchy of PISubBatches in the PI Batch Database.

In the PI Batch Database, each level of the hierarchy is recorded as a module. All levels record their start and end time. PIBatch and PIUnitBatch record the batch ID. In a PIBatch, the Recipe property contains the recipe name. In a PIUnitBatch, the Procedure property contains the name of the corresponding recipe level. If the highest level that a recipe contains is an operation or phase (that is, neither the procedure nor unit procedure levels are defined), the interface creates a parent PIBatch and PIUnitBatch.

By default, the interface creates a set of properties for each level of the hierarchy to contain data relevant to that level, depending on the data provided by the BES. The root property node is named using the batch ID. To override the default properties for a specific level of the recipe hierarchy, use the Event Frame Manager configuration tool to add the default recipe templates and then alter them as needed. To create properties that are not level-specific, define property templates. Events of interest are stored in lists under the appropriate recipe node. Each property under the same node must have a unique name. By default, each property is named "Event_<event count>", where <event count> is the current number of events already stored under a specific node. The PIProperty value can be configured using property templates.

To view batches in the PI Batch Database, use the PI System Management Tools Batch > Batch Database option. The following sections describe how the different levels of the batch hierarchy are stored in the Batch Database.

* **PIBatch**

    The interface creates a PIBatch for each batch found in the data source. The PIBatch corresponds to the procedure in the recipe. Each PIBatch contains one or more PI UnitBatches that correspond to the unit procedures in the recipe.

    Multiple source batches that have identical IDs or a common subset of characters in their ID can be merged into a single PIBatch. The product and recipe properties contain data associated with the first source batch that started the merged PIBatch. The original source batch properties are stored in PIProperties under a node named using the unique ID of the source batch. For each merged source batch, the interface creates a node that is named using the unique ID of the source batch containing the original properties.

    Because a source batch can terminate unexpectedly without proper unloading by the operator, the interface caches batches in local memory for a timeout period, after which the batch is considered abandoned. The interface closes abandoned batches by assigning end time using the latest known timestamp for the batch. The default timeout is 100 days. To change the default timeout, edit the interface settings using PI Event Frame Interface Manager.

* **PIUnitBatch**

    A PIUnitBatch is created for each unit procedure recorded in the data source. The start and end times of a PIUnitBatch are intended to reflect the start and completion of physical processing in a unit, so they require both a start event and an "equipment acquired" event. The unit batch ends when an "end" event or an "equipment released" event is detected. 

    By default, PIUnitBatches contain the batch ID and procedure name from the data source. To override the default, use PI Event Frame Interface Manager to edit the settings. When operation or phase-level recipes are run, the interface uses the operation or phase name as the PIUnitBatch procedure name. 

    If unit procedures on the same unit overlap, the interface closes the conflicting PI UnitBatches. The actual end time for a truncated unit batch is stored in its product property, and the product is appended with the text "_TrueEndUTC=", followed by the actual end time of the unit batch, specified as UTC in seconds. 

* **PISubBatches (Operation, Phase, Phase State and Phase Step)**

    In the batch database, all levels below unit batches are recorded using a hierarchy of subbatches, as follows:
    * Operation: The interface creates a PISubBatch for each child of a unit batch encountered in the data source.
    * Phase: The interface creates a PISubBatch for each child of an operation encountered in the data source.
    * Phase State: The interface creates a PISubBatch for each child of a phase encountered in the data source. The start of new phase state ends the previous phase state, except for the COMPLETE, ABORTED and STOPPED states, which set only the end time.
    * Phase Step: You can configure the interface to create a PISubBatch for each child of a phase state encountered in the data source.
    Subbatches populate parent levels of the hierarchy with the name of the source operation, phase, phase state and phase step as required. 

    Phase steps are not S88-compliant and support for phase steps varies among BES vendors. (ABB800xA, Foxboro IA Series, Siemens SIMATIC, and WonderWare InBatch do not support phase steps.) Phase steps are created beneath the first phase state subbatch named "RUNNING", regardless of whether the parent phase state is ended. The name of phase step start and stop events is read from the data source **DESCRIPT** column. The triggering event is "Report". If the parent phase is not found, phase steps do not trigger the creation of PIBatches, UnitBatches and SubBatches. If the phase step is not explicitly closed by an appropriate event, the interface closes it using the end time of its parent operation. Zero-duration phase steps are ignored. 

