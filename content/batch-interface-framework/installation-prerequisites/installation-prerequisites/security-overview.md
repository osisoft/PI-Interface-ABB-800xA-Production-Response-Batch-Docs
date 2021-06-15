---
uid: BIF_SecurityOverview
---

# Security overview for ABB800xA Production Response Batch 

If you are running PI Data Archive 3.4.380.36 or later, you can take advantage of its support for Windows Integrated Security by running the interface service using a Windows account that has the required permissions on the PI Data server. To configure Windows Integrated Security, use PI SMT to define a mapping that assigns a PI identity that has the required permissions to the user or user\'s group.

**Caution:** To avoid issues with the encryption of credentials be sure to use the same account for the interface service as you use in the PI Event Frames Interface Manager utility. If the interface service logon is not the same as the account that was used to save the credentials in the PI Event Frames Interface Manager utility, decryption of the credentials will fail and the service will exit. This affects credentials stored for login to the data source (e.g. SQL Login) and/or explicit login to AF.

For pre-3.4.380.36 versions of the PI Data Archive, you must create a PI trust for the user that runs the interface and configuration tool. Limit the trust to the hostname or IP address of the interface node and the application name (BIFConfig.exe for the PI Event Frames Interface Manager). Set the following permissions for the user that runs the interface:

* PI Data Archive permissions (**PI SMT**: Browse to **Security > Database Security**)

  * PIBATCH: read/write                                
  * PIMODULES: read/write    
  * PIPOINT read/write 
  * PIAFLINK: read (required for batch-to-event frames migration)

* Per-point security (**PI SMT**: Browse to **Points > Point Builder**)

  * Points created by the interface (using tag templates): Set both PtSecurity and DataSecurity to read/write  
  * If using EFGEN: DataSecurity read access to the active points 

* PI Asset Framework permissions 

  * Database: read/write                    
  * Categories: read/write
  * Element: read/write
  * Element templates: read/write/read data/write data
  * Event frames: read data/write data

To configure batch interfaces to run as a service, the user who runs the PI Event Frames Interface Manager must be in the local Administrators group (administrative privilege is required to create services). The following permissions are required to run the PI Event Frame Manager to configure batch interfaces:

* PI Data Archive permissions

  * PIMODULES: read
  * PIPOINT: read
  * PIARCDATA: read (required for batch-to-event frames migration)

* PI Asset Framework permissions

  * Database: read 
  * Categories: read
  * Elements: read
  * Element templates: read/write
