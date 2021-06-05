---
uid: EventFileMonitorUtility
---

# Event file monitor utility

For interfaces that can use event journal files for a data source, OSIsoft provides a utility that automatically copies new event journals from the directory where the BES creates them to the directory where the interface processes them.
The utility is installed in the same directory as the interface, along with a template Windows command file that you can copy and edit to launch the utility with the desired settings. The executable file name ends with "Sync" (for example, EVTSync.exe).

To configure the utility, copy and edit the batch file, specifying settings using command line parameters as follows:

| Parameter | Description |
| --------- | ----------- |
| /dest=<path> | Full path to destination directory, where the interface processes incoming event journals. |
| /rate=# | Optional rate in seconds to scan source and destination directory. Default scan rate is 30 seconds. This parameter must be an integer value. |
| /src=<path> | Full path to source directory, where the BES creates event journals. |

After specifying settings, invoke the batch file to verify that the utility launches without errors.

To ensure that the utility restarts when the interface node is rebooted, configure a Windows automatic service. To install the service, invoke the executable, specifying the -install switch. For example: EVTSync.exe –install.

To verify that the service was added successfully, check the Microsoft Windows Services control panel.
