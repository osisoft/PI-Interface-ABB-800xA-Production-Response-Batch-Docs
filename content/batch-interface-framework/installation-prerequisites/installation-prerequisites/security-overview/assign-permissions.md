---
uid: BIF_AssignPermissions
---

# Assign permissions for user accounts and PI points

The user that runs the interface requires read/write access to the PI Data Archive. To create event frames and write data to elements and attributes, the user must have permission to connect to the PI Asset Framework. To configure the interface, the user must be in the local
Administrators group. Assign the required permissions to the user that runs the interface and all users who need to run the PI Event Frames Interface Manager configuration tool.

1. Launch PI System Management Tools, and click **Security > Database Security**.

2. For the user account under which the batch interfaces run, set the PIPOINT table to read and write permission.

3. For the user account under which the batch interfaces run,set the PIBACKUP table to read permission.
   
4. For PI points maintained by batch interfaces, set security as follows:

    * Set the PtSecurity to read and write permission for any point that the interface creates.
    * Set the DataSecurity to read and write permission for any point to which the interface writes data.

You can set PI point permissions using PI SMT by choosing **Points > Point Builder**. 

You can change point settings in bulk using the PI SMT plug-in for Microsoft Excel.
