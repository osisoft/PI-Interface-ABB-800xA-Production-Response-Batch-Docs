---
uid: BIF_BatchSetupTab
---

<!-- Mark Bishop 6/8/21: Modified batch framework topic. Deleted all the options that don't apply to 800xA. Added "Create full task hierarchy" -->

# Batch Setup tab

<!-- Topic requires customization for specific interface -->

Use the settings on this tab to identify the elements for various batch settings.

## Alternate PI module path

Select this option to specify an alternate PI Module path or PI AF element path for a particular equipment hierarchy. Select **Find module** to open the Browse to PI Module Path window to navigate to the desired PI module. Select the PI Module to display the path in the Module path field, then select **OK**. 

The interface defaults up to five units to collection:

    RECIPE[1].MODULEPATH=XXX\[UNIT] 
    RECIPE[1].MODULEPATH=XXX\[UNIT2]
    RECIPE[1].MODULEPATH=XXX\[UNIT3]
    RECIPE[1].MODULEPATH=XXX\[UNIT4]
    RECIPE[1].MODULEPATH=XXX\[UNIT5]
    
    RECIPE[2].MODULEPATH=XXX\[UNIT]
    RECIPE[2].MODULEPATH=XXX\[UNIT2]
    RECIPE[2].MODULEPATH=XXX\[UNIT3]
    RECIPE[2].MODULEPATH=XXX\[UNIT4]
    RECIPE[2].MODULEPATH=XXX\[UNIT5]

## Allow deferred units
    
Select this option to enable the creation of unit batches for recipes in units that are allocated at the phase level rather than the unit batch level.

## Create full task hierarchy
    
Select this option to create a full task hierarchy. 
