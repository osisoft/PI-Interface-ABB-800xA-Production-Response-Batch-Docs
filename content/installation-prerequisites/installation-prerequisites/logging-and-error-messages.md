---
uid: BIF_LoggingAndErrorMessages
---

# Logging and error messages

<!-- Static topic. No modifications usually required (REVISED AUGUST 2022-->

The interface logs operational messages during interface startup, data collection and recovery. Additional messages are logged if you enable debugging. 

To view messages, open the Windows Event Viewer on the interface’s installed machine and go to the Applications and Services Logs. Locate the log using the generic interface name. The management of the logs can be done through the Windows Event Viewer.

Streaming messages for a batch interface display in the following format: 

```
{timestamp:yyyy-MM-dd HH:mm:ss.fff} {logLevel,-11} {_iD}: {msg}
```

where {_iD} is the Interface ID instance.

Within the Windows Event Viewer, the Event ID displayed for each batch interface log is the Interface ID instance.

To enable debug output for troubleshooting, launch PI Event Frames Interface Manager, select your interface instance, and go to the Operational Settings tab.

**Operational settings**

Local debug messages (/DB=<#>)

Specifies level of detail for logging as follows:

* 0: Log errors and warnings (default)
* 1: Log errors, warnings and major successes
* 2: Log all messages
* 3: Log all messages including Unirecord diagnostic message

**Command line parameter reference**

/db =[#]

(Optional) Enabled debugging output:

* 0: Log only errors and warnings (default)
* 1: Log errors, warnings and major success messages
* 2: Log all messages (most verbose
* 3: Log all messages including Unirecord diagnostic message

**Log properties**

You can create the Source in the Windows Event Viewer by using the batch interface's source/log name (*see Source/log chart below*) before initially starting the interface. After starting the interface, the Windows Event Viewer creates the Source automatically.

**Note**: If you do not have appropriate permissions to create an event log, it is recommended that you run the interface interactively with an account that has permissions to create an event log. 

To change the log path, increase or decrease the maximum size of the log or modify how the log behaves after reaching the defined maximum event log size, open the Windows Event Viewer and locate the source/log name under Applications and Services Log. Right-click on the source/log name and select **Properties**.

<!-- Source/Log Chart 
| Source/Log Name | Name of Interface |
| BIFConfig | PI Event Frame Interface Manager |
| PIFTBInt | PI Interface for Rockwell Factory Talk Batch |
| PIABB800xA | PI Interface for ABB 800xA Batch |
| ABB800xaPR | PI Interface for ABB 800xA Production Response Batch |
| PIEFGen | PI Event Frames Generator
| PIEMDVB | PI Interface for Emerson DeltaV Batch |
| PIWWInBatch | PI Interface for Wonderware InBatch Batch |
| PIWPASXBatch | PI Interface for Werum PAS-X Batch |
| PIRockwellPharmaSuite | PI Interface for Rockwell PharmaSuite Batch |
| PIEMDVBCS | PI Interface for Emerson Syncade Batch |
| PIGEIB | PI Interface for GE iBatch Batch |
| PISISBatch | PI Interface for Siemens Simatic Batch |  -->

