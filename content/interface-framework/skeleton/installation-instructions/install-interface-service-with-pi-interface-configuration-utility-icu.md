---
uid: SK_InstallInterfaceServiceWithPIInterfaceConfigurationUtilityICU
---

# Install interface service with PI Interface Configuration Utility (ICU)

## Service configuration

The PI Interface Configuration Utility (PI ICU) provides a user interface for creating, editing, and deleting the interface service. The following are descriptions of fields in the PI ICU tool.

### Service name

The Service name box shows the name of the current interface service. This service name is obtained from the interface executable.

### ID

This is the service ID used to distinguish multiple instances of the same interface using the same executable.

## Display name

The Display name text box shows the current Display Name of the interface service. If there is currently no service for the selected interface, the default Display Name is the service name with a "PI-" prefix. Users may specify a different Display Name. OSIsoft suggests that the prefix "PI-" be appended to the beginning of the interface name to indicate that the service is part of the OSIsoft suite of products.

## Log on as

The Log on as box shows the current "Log on as" Windows account of the interface service. If the service is configured to use the NT Service account, the Log on as will have selected "NT Service." Users may specify a different Windows account for the service to use.
    
**Note:** As a security best practice, OSIsoft recommends running this interface service under a lest privileged account, such as a Windows service virtual account, the build-in Network Service account, or a non-administrative account that you create.

PI ICU versions earlier than 1.4.14.x cannot create a service that runs as a Windows built-in service virtual account or the built-in Network Service or NT Service accounts. After ICU creates the interface service, you can change the account with a Windows administrative tool, such as Services on the Control Panel or the sc command-line utility.
    
**Note:** In order to assure that PI buffering functions properly, the user specified in the "Log on as" portion of the **Service** tab must be a member of the "PI Buffering Administrators", or the "PI Buffer Writers" user groups. A virtual service account can be added to those local groups, just like with any local/domain account. Failure to add a user to at least one of these user groups could result in a failure to buffer data. For more details, see the [PI Buffer Subsystem](https://customers.osisoft.com/s/productcontent?id=a7R1000000XyVJUA0) user guide.

## Password

If a Windows User account is entered in the Log on as text box, then a password must be provided in the Password text box, unless the account requires no password.

## Confirm password

If a password is entered in the Password text box, then it must be confirmed in the Confirm password text box.

## Dependencies

The Installed services list is a list of the services currently installed on this machine. Services upon which this interface is dependent should be moved into the Dependencies list using the **Add** button. For example, if API Buffering is enabled, then Bufserv or PIBufss should be selected from the list at the right and added to the list on the left. To remove a service from the list of dependencies, use the **Remove** button, and the service name will be removed from the Dependencies list.

When the interface is started (as a service), the services listed in the dependency list will be verified as running (or an attempt will be made to start them). If the dependent service(s) cannot be started for any reason, then the interface service will not run.
    
**Note:** Please see the PI Log and Windows Event Logger for messages that may indicate the cause for any service not running as expected.

## Add button 

To add a dependency from the list of Installed services, select the dependency name, and click the **Add** button.

## Remove button 

To remove a selected dependency, select the service name in the Dependencies list, and click the **Remove** button. The full name of the service selected in the Installed services list is displayed below the Installed services list box.

## Startup type

The Startup Type indicates whether the interface service will start automatically or needs to be started manually on reboot.

* If the Auto option is selected, the service will be installed to start automatically when the machine reboots.
* If the Manual option is selected, the interface service will not start on reboot, but will require someone to manually start the service.
* If the Disabled option is selected, the service will not start at all.

Generally, interface services are set to start automatically.

## Create

The **Create** button adds the displayed service with the specified Dependencies and with the specified Startup Type.

## Remove

The **Remove** button removes the displayed service. If the service is not currently installed, or if the service is currently running, this button will be grayed out.

## Start or stop service

The toolbar contains a **Start** button and a **Stop** button. If this interface service is not currently installed, these buttons will remain grayed out until the service is added. If this interface service is running, the **Stop** is available. If this service is not running, the **Start** is available.

The status of the interface service is indicated in the lower portion of the PI ICU dialog.

* **Ready** - Status of the ICU
* **Stopped** - Status of the Interface Service
* **`<interfacename>` - Installed** - Service installed or uninstalled
    
    **Note:** `<interfacename>` is the name of your actual interface.
