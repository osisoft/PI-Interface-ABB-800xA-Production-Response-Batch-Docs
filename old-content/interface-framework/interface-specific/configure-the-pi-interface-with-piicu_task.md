---
uid: IS_ConfigureThePIInterfaceWithPIICUTask
---

# Configure the PI Interface for <INTERFACE_NAME> with PI ICU

<!-- Draft comment: Replace images below with screenshots for your interface -->

**Note:** PI ICU requires PI 3.3 or later.

The PI Interface Configuration Utility provides a graphical user interface for configuring PI interfaces. If the interface is configured by the PI ICU, the batch file of the interface (RDBMSPI.bat) will be maintained by the PI ICU and all configuration changes will be kept in that file and the PI Module Database. The procedure below describes the necessary steps for using PI ICU to configure the RDBMSPI Interface.

1. From the PI ICU menu, select Interface, then New Windows Interface Instance from EXE…, and then Browse to the rdbmspi.exe executable file. Then, enter values for Host PI System, Point Source and Interface ID#. A window such as the following results:

    ![alt](https://link)

2. Browse to the RDBMSPI.exe executable file. Then, enter values for Host PI Server/Collective, Point Source , and Interface ID#. Interface name as displayed in the ICU (optional) will have PI- pre-pended to this name and it will be the display name in the services menu.
    
    ![alt](https://link)

    **Note:** In this example the host PI Data server is martinfrpc2. To configure the interface to communicate with a remote PI Data server, select Connections… on the PI ICU Interface menu and select the default server. If the remote node is not present in the list of servers, it can be added.

3. Once the interface is added to PI ICU, near the top of the main PI ICU window, the interface Type should be RDBMSPI. If not, use the drop-down box to change the interface Type to RDBMSPI.

4. Click Apply to enable the PI ICU to manage this instance of the RDBMSPI interface.

    ![alt](https://link)

5. You configure interface-specific settings on the rdbodbc tab, shown in the following figure.

    ![alt](https://link)

    **Note:** A yellow field indicates that an invalid value has been entered, or that a required value has not been entered. 
