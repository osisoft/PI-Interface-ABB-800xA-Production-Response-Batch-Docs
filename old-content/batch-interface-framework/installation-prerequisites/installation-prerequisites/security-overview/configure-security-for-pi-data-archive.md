---
uid: BIF_ConfigureSecurityForPIDataArchive
---

# Configure security for PI Data Archive

<!-- Static topic. No modifications usually required -->

If you are running PI Data Archive 3.4.380.36 or later, you can take advantage of its support for Windows Integrated Security by running the interface service using a Windows account that has the required permissions. To use Windows Integrated Security, use PI System Management Tools to define a mapping that assigns the Windows user (or group) a PI identity that has the required permissions.

For pre-3.4.380.36 versions of the PI Data Archive, you must create a PI trust for the user who runs the interface and configuration tool. For tightest security, limit the trust to the hostname or IP address of the interface node and the application name.

If you are installing the interface on a node other than the PI Data server, you must create trusts to ensure that the configuration tool and the interface have access to the server.

1. To create a trust, launch PI System Management Tools and connect to the target server.

2. Click **Security**, and then click **Mappings & Trusts**.

3. Right-click within the **Trusts** tab, and click **New Trust**.

    The **Add Trust** wizard launches.

4. Enter a meaningful name and description for the trust.

5. Configure the following settings: 
  
    | Program | Type of Trust | Application Name |
    | ------- | ------------- | ---------------- |
    | PI Event Frame Interface Manager | PI-API application  | `BIFConfig.exe` |
    | Interface executable | PI-SDK application | _Executable name_ |
