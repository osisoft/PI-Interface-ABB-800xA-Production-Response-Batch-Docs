---
uid: BIF_SystemRequirements
---

# System requirements

Before installing [!include[product-long](../includes/product-long.md)] [!include[product-version](../includes/product-version.md)] on a target node, ensure that your target environment meets the requirements in this document.

## Software requirements

To install [!include[product-short](../includes/product-short.md)] on the target node, the node must have a supported operating system installed.

Beyond the operating system, [!include[product-short](../includes/product-short.md)] requires PI Server and a batch execution data source. The PI Server and data source can be installed on different remote nodes.

**Tip:** For examples of [!include[product-short](../includes/product-short.md)] system architectures, see <xref:BIF_InterfaceConfiguration>.

### Supported operating systems

[!include[product-short](../includes/product-short.md)] is a 64-bit application that you can install on the following Windows operating systems: 

* Windows 10
* Windows 8.1 (64-bit only)
* Windows Server 2019
* Windows Server 2016
* Windows Server 2012 R2 SP1 (64-bit only)
* Windows Server 2012 (64-bit only)

### PI Server requirements

PI Server 3.3 or later. 

**Recommended:** Install PI Server and [!include[product-long](../includes/product-long.md)] on separate nodes, as installing them on the same node affects performances. Ensure that PI Server is running and accessible from the target interface node.

Install the following server roles on your PI Server:

| Server Role | Version | Required? | Notes |
|-------------|---------|:---------:|-------|
| PI Data Archive | 3.3 or later | Required | N/A  |
| AF Server | 2010 R3 (2.4) or later | Optional | This server role is required if you intend to generate event frames. |

## Supported data sources

[!include[product-short](../includes/product-short.md)] supports the following data sources. These data sources can be installed on the same node as the interface or on remote nodes.

If you install the interface on a separate node from your data sources, ensure that the data sources are running and accessible from the target interface node.

<!-- Add subheaders for each supported data source -->

## User permissions 

The user account that you use to install and configure [!include[product-short](../includes/product-short.md)]:

* Must be a member of the local Administrators group. These permissions are required to create services that [!include[product-short](../includes/product-short.md)] uses.

* Must have read permissions for PI Data Archive and PI Asset Framework. These permission are required to run PI Event Frame Manager, which is used for interface configuration. For information on how to configure these permissions, see <xref:BIF_AssignPermissions>.

## Security Settings

Following installation, [!include[product-short](../includes/product-short.md)] requires a connection to the PI Data Archive. OSIsoft recommends that this connection be secure as possible. Based on the version of PI Data Archive that you are using, OSIsoft recommends different approaches to security.

### PI Data Archive 3.4.380 or later: Configure service account

When installing [!include[product-short](../includes/product-short.md)] in an environment using PI Data Archive 3.4.380 or later, OSIsoft recommends using Windows Integrated Security to operate service accounts for connecting to PI Data Archive. Run the interface service using a service account that has the required permissions on the PI Server.

To configure Windows Integrated Security, use PI System Management Tools (PI SMT) to define a mapping that assigns a PI identity assigned the required permissions to the service account or service account user group. For instructions on how to complete this process, see <xref:BIF_ConfigureSecurityForPIDataArchive>.

**Important!** For [!include[product-short](../includes/product-short.md)] service account operation, use the same service account used for PI Event Frames Interface Manager. This practice prevents issues with encryption of credentials. 

### PI Data Archive earlier than 3.4.380: Create PI trust

When installing [!include[product-short](../includes/product-short.md)] in an environment using a PI Data Archive earlier than 3.4.380, OSISoft recomments creating a PI trust for the user that runs the interface and configuration tool. Limit the trust to the hostname or IP address of the interface node and the application name (BIFConfig.exe for the PI Event Frames Interface Manager). For instructions on how to complete this process, see <xref:BIF_ConfigureSecurityForPIDataArchive>.

## Other requirements and information

### System time

Ensure that the system time is configured correctly on the following nodes:

* The interface target node
* The PI server (if installed on a remote node)
* The data source (if installed on a remote node)

### Installation drive

OSIsoft recommends that you install the interface on a drive other than C:, which you should reserve for the operating system.