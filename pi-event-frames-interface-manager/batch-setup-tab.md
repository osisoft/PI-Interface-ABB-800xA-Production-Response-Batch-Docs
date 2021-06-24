---
uid: BIF_BatchSetupTab
---

# Batch Setup tab

<!-- Topic requires customization for specific interface -->

Use the settings on this tab to identify the elements for various batch settings.

## Report as step

Select this option and then set a Start and an End date. 

## Alternate PI module path

Select this option to specify an alternate PI Module path or PI AF element path for a particular equipment hierarchy. Click Find module to open the Browse to PI Module Path window to navigate to the desired PI module. Select the PI Module to display the path in the Module path field, then click OK. 

## Disable arbitration

Select this option to create unit batches based solely on source batch recipe data. Select this option when the source Batch Executive System (BES) provides batch data without equipment arbitration data. 

## Disable arbitration counters
    
Select this option to direct the interface to release a unit on the first resource release event even if the number of acquire events is higher than the number of release events. 

## True batch start date
    
Select this option to use top level recipe start/end events for creating batch objects. 

## Allow deferred units
    
Select this option to enable the creation of unit batches for recipes in units that are allocated at the phase level rather than the unit batch level.
