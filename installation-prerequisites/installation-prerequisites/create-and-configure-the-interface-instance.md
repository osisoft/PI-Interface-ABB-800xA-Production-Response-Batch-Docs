---
uid: BIF_CreateAndConfigureInterfaceInstance
---

# Create and configure the interface instance

<!-- Static topic. No modifications usually required -->

For each instance you create, settings are stored in a separate Windows command (.bat) file and an initialization (.ini) file in the [!include[%ProgramData%](../../includes/dir-long.md)] directory. The batch file launches the interface, specifying settings as command line parameters. The initialization file also contains settings, and it defines templates that determine how data from the data source is stored in the PI System. To configure settings for interfaces, use the PI Event Frames Interface Manager. Use this tool even if you are configuring the interface to store data in the PI Batch Database rather than event frames.

A single batch interface instance can be configured to read from multiple data sources. This capability enables you to handle distributed batch processing scenarios, where multiple batch execution systems cooperate in the manufacturing of a single batch. If you configure multiple data sources, all data sources must be the same type, either event files or SQL databases.

**Note:** Each [!include[interface](../../includes/product-long.md] instance must run under a unique service account. For additional information, see [Can I use the same service account to run multiple instances of EF-generating interfaces?](https://osisoft.lightning.force.com/lightning/r/Knowledge__kav/ka01I000000fZCGQA2/view).

To launch the PI Event Frames Interface Manager, click **Start > All Programs > PI System > PI Event Frames Interface Manager**. For detailed information about the settings on each tab, see [PI Event Frames Interface Manager](xref:BIF_PIEventFramesInterfaceManager).

To create an instance of the interface, perform the following steps using PI Event Frames Interface Manager:

1. On the **Interface Selection** tab, click **Add Interface**. A list of installed interfaces displays.

2. Choose the interface that you want to configure, and specify a service ID number and description if desired.

3. Click **OK**.            

4. On the **Server Information** tab, specify settings for your PI servers.

    If you intend to create event frames, check **Create event  frames** and specify the PI Asset server and AF database.

5. On the **Source** tab, configure the settings for the data source (the BES).

    Note that you can configure multiple data sources for the same interface instance.
    
6. On the **Templates** tab, define templates for tags, properties and the batch recipe.

    For details, see [Templates for mapping data source events](xref:BIF_TemplatesForMappingDataSourceEvents).

7. On the **Filters** tab, specify any batch levels from the data source that you do not want the interface to process.

8. On the **Time Settings** tab, configure retry and timeout settings.

9. On the **Batch Setup** tab, configure settings according to the requirements of your batch execution system.

10. On the **Operational Settings** tab, configure settings to determine how batch data is recorded, and any interface-specific settings required.

11. To save your changes, click **Save Settings**.
