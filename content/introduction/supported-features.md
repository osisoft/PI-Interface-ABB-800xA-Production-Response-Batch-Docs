---
uid: BIF_SupportedFeatures
---

# Supported features

<!-- Add custom intro for interface -->


<!-- Content below applies to all batch interfaces -->

| Feature | Support |
| ------- | ------- |
| Part Number | <UPDATE_FOR_INTERFACE> |
| Auto-creates PI Points and equipment assets? | Yes |
| Point Builder Utility | No |
| Stores batch data in PIBatch Database and PI Module Database | No |
| Stores batch data in PI AF | Yes |
| Supports equipment arbitration events | No |
| Supports n-way buffering | Yes|
| ICU Control | No (use PI Event Frame Interface Manager configuration tool) |
| PI Point Data Types | Int32/ Float32/ String |
| Sub-second Timestamps | Yes |
| Sub-second Scan Classes | No |
| Automatically Incorporates Changes to PI Point Attributes | No |
| Exception Reporting | No |
| Outputs from PI | No |
| Inputs to PI | Event and Scan-based |
| Supports Questionable Bit | No |
| Supports Multi-character Pointsource | Yes |
| Maximum Point Count | No maximum |
| Uses AF SDK | Yes: version 2.5.x or higher required |
| PINet String Support | N/A |
| Source of Timestamps | BES (not system time on interface node) |
| History Recovery | Yes |
| UniInt-based | No |
| Disconnected Startup | No |
| SetDeviceStatus | Yes |
| Failover | No |
| Vendor Software Required on PI Interface Node | No |
| Vendor Hardware Required | No |
| Additional PI Software Included with Interface | Yes  |
| Device Point Types | The interface receives data from source as strings and coerces the data into numerical types according to tag templates, if defined.|
| Serial-Based Interface | No |

## Equipment arbitration events

This PI Batch Interface runs against a BES or MES that supports equipment arbitration events. These events provide precise time stamps for the start and end times of unit batches. Individual installations of BES or MES that support equipment arbitration events may not be configured to provide such events. If the BES or MES supports equipment arbitration events but is configured not to provide them, use the following command line parameter: [/noarbitration](xref:BIF_CommandLineParameterReference#noarbitration). 

Using `/noarbitration` ensures that the interface:

* Sets the start time of unit batches using the timestamp of the "Unit Procedure Started" event or the start of the next operation or phase for the unit, whichever is later.

* Sets the end time of unit batches using the timestamp of the "Unit Procedure Finished" event or the end of the last operation or phase for the unit, whichever is earlier.

* For operation-level recipes, the interface uses the start time of the first phase as the start time for the parent operation and unit batch, and the timestamp of the "Operation Finished" message as the end time of the phase, operation and unit batch.

## History recovery

You can stop the interface without losing any data, because the data is persistent in the data source. Data recovery is limited by the history available from the BES, the number of licensed PI tags, and the size and time frame of the PI archives into which data is recovered.

## Device status tag

This string tag contains information about communication between the interface and the data source. This tag is evaluated only while the heartbeat tag is updating and is updated on startup, change, and shutdown.

During normal operation, the tag contains the digital state set value "Good", indicating that the interface is communicating properly with the data source. Otherwise, the tag contains a string indicating status.

The following table lists standard status strings.

| Message | Description |
|--|--|
| `1 Starting` | The interface is starting. |
| `2 Connected / No Data` | The interface is connected to the data source but is not capable or reading or writing data to the foreign device. |
| `3 n device(s) in error` | The interface is not able to communicate with the specified number of devices. Usually includes additional interface-specific details. |
| `4 Intf Shutdown` | The interface is shutting down. |
| `5 interface_specific_message` | Message specific to the interface. |
