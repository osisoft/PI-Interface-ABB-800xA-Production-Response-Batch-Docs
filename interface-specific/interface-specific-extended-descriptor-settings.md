---
uid: IS_InterfaceSpecificExtendedDescriptorSettings
---

# Interface-specific ExDesc (extended descriptor) settings

| Keyword | Description | Example |
|:-|:-|:-|
| PERFORMANCE_POINT | When set, such point stores the amount of time, in seconds, that it takes an interface to complete a scan for a particular scan class. The lower the scan time, the better the performance. | PERFORMANCE_POINT For details, refer to the [PI Universal Interface (UniInt) User Guide](https://techsupport.osisoft.com/Downloads/All-Downloads/All-Groups/All-Products/All-Categories/Current-Version/uniint/). |
| TRIG or EVENT | For event-driven input points: each time the specified point changes, the SQL query is executed. If the point name contains spaces, you must enclose it in single quotes. If there are subsequent parameters, you must specify a comma after the /EVENT specification. Valid conditions:<br><br>&bull; anychange<br>&bull; increment<br>&bull; decrement<br>&bull; nonzero <br><br>For details about defining event- driven points, refer to the [PI Universal Interface (UniInt) User Guide](https://techsupport.osisoft.com/Downloads/All-Downloads/All-Groups/All-Products/All-Categories/Current-Version/uniint/). | /EVENT=sinusoid, … or <br>/EVENT=sinusoid anychange, … |
