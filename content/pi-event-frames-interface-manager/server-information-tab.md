---
uid: BIF_ServerInformationTab
---

# Server Information tab

<!-- Customized for ABB 800xA. -->

The **Server Information** tab is where you configure the PI Data server and PI Asset server that you intend to use with the interface instance. The interface can generate either batches in the PI Batch Database or event frames in the PI Asset Framework.

## PI Data server (/HOST) settings

The PI Data server specified under PI Data server specifies the server to which the interface sends batch data. _Host_ is the IP address or fully-qualified domain name of the PI Data server. If the server that you want to use is not listed in the drop-down menu, add it to the known servers table using the [About PI-SDK utility](https://livelibrary.osisoft.com/LiveLibrary/content/en/server-v5/GUID-92B81C3E-8C8C-4670-AFFE-033F45A9DB5C). 

If you are using a PI Data Archive version prior to 3.4.380.36, select **Use explicit log** in to specify a **PI user name** and **PI password**.

**Note:** When you use an explicit login to authenticate with PI Data server, [!include[interface](../includes/product-short.md)] stores the credentials you enter in Windows Credential Manager. For details, see <xref:BIF_WindowsCredentialManagerAuthentication>.

If you are using a PI Data Archive version 3.4.380.36 and higher, use Windows Integrated Security for authentication. Ensure that the Windows account that runs the interface has sufficient permissions on the PI Data server to write data to PI points.

**Note:** You must then configure a trust that permits access for the user that runs the interface service.

## PI Asset server settings

In this section you configure PI Asset Framework configuration settings. 

Select **Create event frames in PI Asset Framework** to create event frames in PI Asset Framework, instead of creating batches in the PI Batch Database. 

The PI Asset server and PI Asset Framework database are displayed in the **Host and Database** (/AFHOST and /AFDATABASE) field. Click **Select Asset server** to open the Select Database window to choose an alternative server. 

<!-- 

Mark Bishop 6/11/21: Commenting out content that doesn't apply to ABB 800xA

Under **Enable Auto Checkin**, select from the following options:

* **None**: The interface will do nothing with checked out Event Frames on a restart/reconnection.
* **Checkin**: The interface will check in any checked out Event Frames on a restart/reconnection.
* **Rollback**: The interface will undo any checked out Event Frames on a restart/reconnection.
        
**Note:** If the same user account is running multiple batch interfaces, our recommendation is to set **Enable Auto Checkin** to None. The OSIsoft best practice is to have a separate service account for each batch interface. 

-->

If you are not using Windows Integrated Security for authentication, check **User explicit login for PI Asset Framework** and enter the **Windows account** and **Password** for the Windows user account that you intend to use to connect to PI Asset Framework.

**Note:** When you use an explicit login to authenticate with PI Asset Framework, [!include[interface](../includes/product-short.md)] stores the credentials you enter in Windows Credential Manager. For details, see <xref:BIF_WindowsCredentialManagerAuthentication>.
