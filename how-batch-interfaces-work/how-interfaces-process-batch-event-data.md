---
uid: BIF_HowInterfacesProcessBatchEventData
---

# How batch interfaces process event data

The interface processes start and end events for each level. The level at which a recipe executes depends on the equipment it requires. For example, a batch-level recipe is most likely composed of unit procedures and procedures executed on multiple different units. By contrast, an operation-level recipe might execute a set of phases in a single unit. The interface automatically creates PIBatches (or level 1 events) and PIUnitBatches (or level 2 events) for operation- and lower-level recipes, even though the events in the data source do not include these levels. The BES events that trigger the start and end of each level are vendor-specific. For details, refer to the vendor-specific information in this document.

When you configure the interface to generate event frames in PI AF, the interface creates a set of event frame templates in the target database, one template for each level in the standard S88 batch hierarchy. You can modify the templates to customize the data that is stored in the generated event frames. The interface creates equipment assets in the Module Database or PI AF (depending on where you're storing batch data) based on allocation events from the BES, and populates the attributes of those assets with relevant data.
    
**Caution**: To ensure compatibility with RtReports, any custom Event Frame batch template used must be derived from a default Batch Interface Event Frame Template.
