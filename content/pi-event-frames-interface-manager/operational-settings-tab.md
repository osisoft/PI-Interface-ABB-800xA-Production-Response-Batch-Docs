---
uid: BIF_OperationalSettingsTab
---

# Operational Settings tab

<!-- Mark Bishop 6/8/21: Customized for ABB 800xA. -->

Modify the settings on the Operational Settings tab to configure the interface mode and other related settings.

## Operational Settings

### Realtime mode (/MODE=<mode>)
    
Interface modes are selected from the drop-down menu. Options are described in the table below. 
    
For the Recovery, Statistics, Preprocess, and Delete options, you can identify a **Start Time** and an **End Time**. Click the calendar icon associated with each field to select dates and times.
    
| Mode | Description |
| ---- | ----------- |
| Realtime (default) | Scan data source to collect data in realtime. |
| Recovery | Scan data source and generate or correct events accordingly. Always starts in recovery mode, then switches to realtime mode. |
| Statistics | Compare data source history against events and report results without updating any data. |
| Preprocess | Source data is written to the PI Data archives with timestamps earlier than those written to the primary PI archive.<br><br>**Note:** This mode requires that you use the offline archive utility to reprocess older archives. This is done after completion when the interface stops. |
| Delete | Delete events for a specified period. |

<!-- Removed Content from delete row:

<br><br>**Note:** Selecting "Delete mode" limits you to specifying a Start Time only. In the GUI, the End Time is always specified with "*" asterisk symbol, a dereference operator pointed to by the variable's value.<br><br>The interface allows for "spot deletion", meaning the deletion of event frames from within a specific time window. For example, you may have a scenario where you have received "junk data" from previous days. Spot deletion allows you to delete event frames back to the date when you began receiving unusable data. The GUI does not provide the means to specify both ends of the time window that you wish to delete. That can be done through edits to the configuration file.<br><br>An RST for Delete mode can still be specified in the initialization file, but the GUI will always disable spot deletion.

-->
### Perform one scan then stop (/SINGLERUN)
    
The interface performs one scan of active points, then exits. 

### Print result of first scan to file (/PRINT=<file name>)
    
Print the results of the first scan to the specified text file. The results include the event frame hierarchy tree, the tag list, and the equipment tree. This parameter is designed primarily for troubleshooting and configuration testing when the interface is run in statistics mode. Enter a name for the scan in the field provided (for example, `C:\Users\jdoe\Documents\PIWPASXBatch1_stat.dat`). You have the option of clicking **Select file** to browse to the file path. 

### Local debug messages (/DB=<#>)

Specifies level of detail for logging as follows:

* 0: Log errors and warnings (default)
* 1: Log errors, warnings and major successes
* 2: Log all messages
* 3: Log all messages including Unirecord diagnostic messages

### Numeric settings (/NS=<lang>)

Configures how numeric values are formatted by the interface, to enable the interface to properly interpret numeric values based on the machine's regional setting or a user-specified language. Default is "English (United States)". 

### Interface ID (/ID=x)
    
Specifies the numeric interface instance identifier (maximum nine digits). To detect PI points maintained by the interface instance, the interface matches this setting against the value in the points' Location1 attribute. 

### Point source (/PS=x)
    
Point source for the interface instance. Point source is not case sensitive. Corresponds to the PointSource attribute of individual PI points. The interface loads PI points with the same point source.

<!-- Mark Bishop 6/8/21: Added "Associate all reference...". -->

### Associate all reference elements with child Event Frames (/DPRETC)
    
When creating event frames in PI AF, by default all reference elements are associated with child event frames. 

<!-- WEM 4/7/22: This interface doesn't support failover
## Failover settings

### Failover tag (/FAILOVERTAG=x)

The PI tag to be used to coordinate failover. Click the icon to open the Tag search window, where you provide the name of the tag in the **Tag Mask** field. The tag that you select displays in the **Failover tag** field of PI Event Frames Interface Manager. 

### Failover identifier (/FAILOVERID=x)
    
A unique identifier for this interface instance, used to coordinate which instance is primary. 

### Failover swap time (/SWAPTIME=<seconds>)

Select to specify how long an interface can be inactive before failover to another instance occurs. The default is 300 seconds. 
-->
    
## Security settings

### Specify point security (/PTSEC=x)

Override the default point security created by the interface. Click **Change** to open the Change security window. There you can select from or add to the options listed, and specify read/write authorizations for each. Click **OK** to change point security. 

### Specify data security (/DATASEC=x)

Override the default data security of PI points created by the interface. Click Change to open the Change security window. 
