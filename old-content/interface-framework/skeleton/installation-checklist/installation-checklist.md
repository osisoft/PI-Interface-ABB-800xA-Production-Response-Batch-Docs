---
uid: SK_InstallationChecklist
---

# Installation checklist

It is strongly recommended that you read this user guide in detail before installing your interface, particularly if this is your first PI interface installation.

If you are familiar with running PI data collection interface programs, this section should help you get the interface up and running.
    
**Note:** This checklist summarizes the steps for installing an interface. Some tasks may not be required if you have previously installed another interface on the same machine. For example, you only have to configure one instance of buffering for every interface node regardless of how many interfaces run on that node.

1. Determine if you need to install a Read-only or Read-write version of the interface. Refer to <xref:SK_ReadOnlyAndWriteOnlyInterfaces>.
    
    **Note:** Some interfaces are provided only in read-write versions. Read-write interfaces involve security risks that you may want to circumvent by disabling read-write updates to your data source. Refer to <xref:SK_DisableReadWriteUpdatesToTheDataSource>.

2. Ensure that you have permissions to use PI System Management Tool (SMT) to create new points and edit security settings in PI Data Archive. See your system administrator if you find you need permissions.
    
    **Note:** You do not need to run PI SMT on the same computer on which you run this interface.

3. Use PI SMT to edit the PI Data Archive Trust table to allow the interface to read attributes and point data, required if you are running the interface on an interface computer. For more information, refer to [PI Data Archive tables and primary keys](https://livelibrary.osisoft.com/LiveLibrary/content/en/server-v7/GUID-86C0A2BB-7364-4355-9890-C4EC65DAD6A2#) in [PI Server 2016](https://livelibrary.osisoft.com/LiveLibrary/content/en/server-v7/GUID-86C0A2BB-7364-4355-9890-C4EC65DAD6A2#addHistory=true&filename=GUID-B4F5E027-DE91-4E72-B603-84EF4C7525DB.xml&docid=GUID-EA52D970-5D4E-44E6-BA4C-08A3F8CDCD8D&inner_id=&tid=&query=&scope=&resource=&toc=false&eventType=lcContent.loadDocGUID-EA52D970-5D4E-44E6-BA4C-08A3F8CDCD8D).
    
    **Note:** If a buffering application is not running on the interface computer, the PI trust must allow the interface to write data.

4. Check the computer's time zone properties. Incorrect time zone configuration can cause the PI Data Archive to reject the data that the interface writes. For example, if the clock on the interface node is significantly ahead (10 minutes or more) of the clock on the PI Server node, then the PI Server will reject those incoming values as they are from the future.
   
5. Run the full interface setup executable, which includes the Interface installation and PI ICU installation kits.
    
    **Note:** Running the Interface setup executable installs the PI Modbus Ethernet Interface, PI ICU, PI API, and PI SDK.

6. Complete the procedure to establish data collection. Refer to <xref:SK_DataCollectionSteps>.

7. (Optional) Perform interface diagnostics to determine the configuration required to gather data.

8. Consider the applicability of advanced interface features. Refer to the _UniInt failover configuration overview section_ of the [PI Universal Interface (UniInt) Framework User Guide](https://livelibrary.osisoft.com/LiveLibrary/web/pub.xql?action=publist_home&pub_category=PI-Universal-Interface-(UniInt)-Framework) for additional information.
