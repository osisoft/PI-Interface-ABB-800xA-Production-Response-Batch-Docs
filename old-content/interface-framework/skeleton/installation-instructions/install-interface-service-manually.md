---
uid: SK_InstallInterfaceServiceManually
---

# Install interface service manually

You can access help for installing the interface as a service at any time by using the following command:

`interfacename.exe /help`

1. Open a Windows command prompt window and change the directory to where the interfacename.exe executable is located. Consult the following table to determine the appropriate service installation command.
    
    **Note:** In the following Windows service installation commands, you may use either a slash (/) or dash (-) as the delimiter.

    | Commands with Bufserv implemented |  |
    |--|--|
    | Manual service | `<interfacename>.exe /install /depend "tcpip bufserv"` |
    | Automatic service | `interfacename.exe /install /auto /depend "tcpip bufserv"` |
    | Automatic service with service ID | `interfacename.exe /serviceid x /install /auto /depend "tcpip bufserv"` |

    | Commands without Bufserv implemented |  |
    |--|--|
    | Manual service | `interfacename.exe /install /depend tcpip` |
    | Automatic service | `interfacename.exe /install /auto /depend tcpip` |
    | Automatic service with service ID | `interfacename.exe /serviceid X /install /auto /depend tcpip` |

    **Note:** When specifying service ID, the user must include an ID number. It is suggested that this number correspond to the interface ID ( /id) parameter found in the interface `.bat` file.

2. Check the Services control panel to verify that the service was added successfully.

    The services control panel can be used at any time to change the interface from an automatic service to a manual service or vice versa. The service installation commands in this section create an interface service that runs under a low-privilege built-in account.

    On Windows 7 and Server 2012 and later, the service logs on as the service virtual account. For earlier versions of Windows, the service logs on as Network Service.
    
    **Note:** For best security, run this interface service under an account with minimum privileges, such as a Windows service virtual account, the built-in Network Service account, or a non-administrative account that you create.

    The services control panel can change the account that the interface service runs under. Changing the account while the interface service is running does not take effect until the interface service is restarted.
