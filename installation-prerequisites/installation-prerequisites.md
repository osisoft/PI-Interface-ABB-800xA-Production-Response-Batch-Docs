---
uid: BIF_InstallationPrerequisites
---

# Prerequisites for installing PI Interface for EMBDVB

Minimum required versions of PI System software: PI Server 3.3 and PI AF 2010 R3 (2.4)

Before installing and configuring, ensure that the following
prerequisites are met:

* Verify that the PI Data Archive is running and that the PI Data server is accessible from the computer where you intend to run the interface (the interface node).

* If you intended to generate event frames, make sure that the PI Asset Framework is running and that the PI Asset server is accessible from the interface node.

* Ensure that the system time on all these computers is correct.

* Verify that your batch execution system is up and running and that the data source is accessible from the interface node.

To install the interface, download and run its setup kit. By default, the interface is installed in an interface-specific folder in the following location: %PIHOME%\\Interfaces\\

The interface installation directory contains all the files and folders required to configure and run the interface, and includes example configurations.

The interface can run on the same computer as the BES or on a dedicated node. To avoid affecting the performance of the PI Data Archive, do not install the interface on the PI Data server. When installing the interface, reserve the C: drive for the operating system, and install the interface on another drive.

If the data source is Microsoft SQL Server, you must install the Microsoft SQL Native Client on the interface node. You can download the client from the MSDN web site. If the data source is an Oracle database, you must install the corresponding version of Oracle Provider for OLE DB.

To configure the interface, use the PI Event Frame Manager configuration tool.

**NOTE:** If you intend to run the interface as a Windows service and need to configure explicit login settings for your BES data sources, ensure that the account you configure for the service is the same account you use to run the configuration tool.
