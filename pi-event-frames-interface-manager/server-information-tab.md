---
uid: BIF_ServerInformationTab
---

# Server Information tab

<!-- Static topic. No modifications usually required -->

The **Server Information** tab is where you configure the PI Data server and PI Asset server that you intend to use with the interface instance. The interface generates event frames in the PI Asset Framework.

## PI Data server (/HOST) settings

The PI Data server specified under PI Data server specifies the server to which the interface sends tag data. _Host_ is the IP address or fully-qualified domain name of the PI Data server or PI Collective. If the server that you want to use is not listed in the drop-down menu, add it to the known servers table using the [PI System Explorer](https://docs.aveva.com/bundle/pi-server-af-pse/page/1019495.html). 

If you are using a PI Data Archive version prior to 3.4.380.36, select **Use explicit log** in to specify a **PI user name** and **PI password**.

**Note:** When you use an explicit login to authenticate with PI Data server, [!include[interface](../includes/product-short.md)] stores the credentials you enter in Windows Credential Manager. For details, see <xref:BIF_WindowsCredentialManagerAuthentication>.

If you are using a PI Data Archive version 3.4.380.36 and higher, use Windows Integrated Security for authentication. Ensure that the Windows account that runs the interface has sufficient permissions on the PI Data server to write data to PI points.

**Note:** You must then configure a trust that permits access for the user that runs the interface service.

## PI Asset server settings

In this section you configure PI Asset Framework configuration settings. 

Select **Create event frames in PI Asset Framework** to create event frames in PI Asset Framework, instead of creating batches in the PI Batch Database. 

The PI Asset server and PI Asset Framework database are displayed in the **Host and Database** (/AFHOST and /AFDATABASE) field. Click **Select Asset server** to open the Select Database window to choose an alternative server. 

Select the **Enable Batch Interface Element** check box to create a new element that contains the Interface Health Tag information.

Interface Health Tags collect batch statistics for the interface, such items as process time for unirecords or the number of unirecords in a batch.

**Note:** The naming convention used for a Batch Interface Element is *(InterfaceInstanceName)_(InterfaceID)*_BatchStatistics.
        
Click **Select Parent Element** to open a dialog box to search for a parent to host the new element. After locating the parent, select OK to return to the Server Information tab.

**Note:** A Batch Interface Element can be created in a separate Asset Framework database. 

Under **Enable Auto Check In**, select from the following options:

* **None**: The interface will do nothing with checked out Event Frames on a restart/reconnection.
* **Check In**: The interface will check in any checked out Event Frames on a restart/reconnection.
* **Rollback**: The interface will undo any checked out Event Frames on a restart/reconnection.
        
**Note:** If the same user account is running multiple batch interfaces, our recommendation is to set **Enable Auto Check In** to None. The OSIsoft best practice is to have a separate service account for each batch interface.

If you are not using Windows Integrated Security for authentication, check **User explicit login for PI Asset Framework** and enter the **Windows account** and **Password** for the Windows user account that you intend to use to connect to PI Asset Framework.

**Note:** When you use an explicit login to authenticate with PI Asset Framework, [!include[interface](../includes/product-short.md)] stores the credentials you enter in Windows Credential Manager. For details, see <xref:BIF_WindowsCredentialManagerAuthentication>.
