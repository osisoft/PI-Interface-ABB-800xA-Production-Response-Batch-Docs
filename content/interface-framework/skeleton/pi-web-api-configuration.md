---
uid: SK_PIWebAPIConfiguration
---

# PIWebAPI Configuration

A general example of the PIWebAPI endpoint configuration is shown here:

```text
EndPointType=PIWebAPI
HostName=MyHostName
Port=####
User=MyUserName
Password=MyPassword
```

Here are the PIWebAPI configuration parameters defined:

* EndPointType=PIWebAPI

    This line signifies the start of a PIWebAPI configuration.

* HostName

    The name of the server hosting the PIWebAPI service.

* Port

    PIWebAPI must listen for HTTPS traffic on a communication port; typically port 443. The valid range is between 1 and 65535. The number in this configuration file will match the number specified when PIWebAPI was installed on the node.

* User

    The identity of the user set up with PIWebAPI. This field will be erased from the config file once the service is started.

* Password

    The password set up with PIWebAPI. This field will be erased from the config file once the service is started. 
