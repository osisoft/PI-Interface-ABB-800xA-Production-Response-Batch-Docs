---
uid: SK_DataCollectionSteps
---

# Data Collection Steps

Complete the following steps to establish PI Data Archive data collection.

1. Use PI ICU to configure a new instance of the interface.

    The essential startup parameters for this interface are:

      * Point Source (/PS=x)
      * Interface ID (/ID=#)
      * PI Data Archive (/Host=host:port)
      * Scan Class (/F=##:##:##,offset)

2. Use a data source-specific connection tool to confirm connection between the interface computer and the device.

3. Define the appropriate digital state sets, if you use digital points.

4. Add the X, Y, and Z states to the system digital state set.
        
5. Build input tags and, if desired, output tags for this interface.
    
    PtSecurity must permit read access for the PI identity, group, or user configured in the PI trust that is used by the interface. DataSecurity must permit read access (buffering enabled) or read/write access (unbuffered) for the PI identity, group, or user configured in the PI trust that is used by the interface.
    
    **Note:** When buffering is configured, the DataSecurity attribute must permit write access for the buffering application's PI trust or mapping. DataSecurity write permission for the interface's PI trust is required only when buffering is not configured.

6. Start the interface interactively and confirm its successful connection to the PI Data Archive without buffering. (The DataSecurity attribute for interface points must permit write access for the interface's PI trust.)

7. Configure the interface to run as a Windows service. Confirm that the interface runs properly as a service.

8. Confirm that the interface collects data successfully.

9. If output points are required, confirm that output points update the correct values in the data source. Create an output point whitelist file for the interface instance. For information, see the topic "Secure output points using a whitelist file" in the [PI Universal Interface (UniInt) user guide](https://livelibrary.osisoft.com/LiveLibrary/content/en/uni-int-v2/GUID-B76FDAF0-159B-4D95-9964-D49DA0CDE83F#).
