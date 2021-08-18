---
uid: Overview
---

# Overview

PI Interface for ABB 800xA Production Response Batch is a new ABB batch interface that relies on ABB client tools to retrieve ABB tasks in the form of data streams. Currently, OSIsoft offers two ABB 800xA Batch interfaces: one for the Production Data Log (an Oracle-based 800xA backend), and one for Production Response (SQL-based 800xA backend). Version 4.2.3 of PI Interface for ABB 800xA Production Response Batch supports version 6.0.3.2 and 6.0.3.3 of the ABB 800xA Production Response system. In addition, this interface requires the 800xA Batch Production Response SDK to be installed as a prerequisite.

## Components

PI Interface for ABB 800xA Production Response Batch uses ABB client tools to collect and transfer ABB data into a complete batch tree.
Enabling this interface requires user installation of the ABB Ability Manufacturing Operations Management Process Intelligence SDK, as well as the following DLL files:

* ABB.SDS.Desktop.dll
* ABB.SDS.dll
* ABB.SDS.S95PR.Accessor.dll
* ABB.SDS.Server.Accessors.dll
* ABB.SDS.Server.Accessors.Interfaces.dll
* ABB.SDS.Server.Client.dll
* Castle.Core.dll
* VtrinLib.dll
* Newtonsoft.Json.dll

For the procedure for installing these DLL files, see <xref:InstallDLLsforABB800xA>. 

**Note:** This interface can only create Event Frames in the PI Asset Framework server and cannot create batches in the PI Batch Database.
