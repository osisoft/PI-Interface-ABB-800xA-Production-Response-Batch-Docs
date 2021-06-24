---
uid: IS_ConfigureTheInterfaceWithPIICU
---

# Configure the interface with PI ICU
    
<!-- Draft comment: Replace images below with screenshots for your interface -->

**Note:** PI ICU requires PI 3.3 or later.

The PI Interface Configuration Utility provides a graphical user interface for configuring PI Interfaces. If the interface is configured by the PI ICU, the batch file of the interface (<`interfacename>.bat`) will be maintained by the PI ICU and all configuration changes will be kept in that file and the PI Module Database. The procedure below describes the necessary steps for using PI ICU to configure the Interface.

1. From the PI ICU menu, select Interface> NewWindows Interface Instance from EXE

1. Browse to the `<interfacename>`.exe executable file.

1. Enter values for Host PI Data Server, Point Source and Interface ID#.

    The Configure a New Interface window opens.

    ![image]()
    
    **Note:** Interface name as displayed in the ICU (optional) will have PI- prepended to this name and it will be the display name in the services menu.

1. Click Add.

    The PI ICU Register Interface window opens.

    ![image]()
    
    In this example, the host PI Data server is srvhv4. To configure the interface to communicate with a remote PI Data server, select Connections on the PI ICU Interface menu and select the default server. If the remote node is not present in the list of servers, it can be added. Once the interface is added to PI ICU, near the top of the main PI ICU window, the interface type should be `<interfacename>`. If not, use the drop-down box to change the interface type to `<interfacename>`.

1. Click Apply.

    The PI ICU gets enabled to manage this instance of the SattLine interface and specify the desired scan classes.

    ![image]()

1. Make selections in the interface-specific tab (that is "`<interfacename>`") that allow the user to enter values for the startup parameters that are particular to the `<interfacename>` Interface.

1. Configure the interface-specific settings on the `<interfacename>` tab as shown in the following figure.

    **Note:** A yellow field indicates that an invalid value has been entered.

    ![image]()
    
    | Setting | Description |
    |:-|:-|
    | Output log file path: (/Output=<UNC Path>) | The /output parameter is used to specify the Interface-specific error log file name and location. |
    | Site batch info (/SBI=SBISystem:SBIJournal) | Site batch info system and journal specification. |
    | Close journals for scan classes (CS List) (/CJ=#,#,#) | The comma separated list of scan classes, which should close their journals after their data has been fetched and reopen during the next scan. |
    | Use MaxGetPending (First scan only) (/MaxGP1=#) | Time in seconds the interface will wait until the events are delivered during the first scan class. |
    | Use MaxGetPending (All Scan Classes) (/MaxGP2=#) | Time in seconds the interface will wait until the events are delivered during any other scan class except the first one. |
    | Maximum Time for historical recovery (/MaxHist=#) | Maximum time in days for history recovery; default - 10 days. The interface will not attempt to recover longer intervals (than specified through /MaxHist), independent of the time in the snapshot of the given PI tag. |
    | Debug level (/Deb=#) | The interface prints additional information into the interface specific log file, depending on the debug level used. The amount of log information increases with the debug number as specified in the table below (see - the /DEB=# command line parameter). |
    | No historical loading (/NoHist) | Prevents the historical data recovery. The first query against the `<interfacename>` system will use the start time = current time. Without this start-up parameter, the interface will start asking for data from the - time of the PI Snapshot. |
    | Use timestamp with milliseconds (/UseMS) | Does not strip (cut) the subsecond part from timestamps obtained from the `<interfacename>` Journals. |
    | Parallel reading (/ParRed) | Forces reading from two `<interfacename>` servers. |
    | Maximum time for historical recovery for PI SBI LogTags (/MaxHistSBI=#) | Use 10 days recovery time interval for the PI SBI Log Tag. |
    | Additional parameters | The Additional parameters section is provided for any parameters that may be required in the future. |
