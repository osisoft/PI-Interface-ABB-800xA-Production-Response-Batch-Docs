---
uid: IS_ExDesc
---

# ExDesc (extended descriptor)

<!-- Draft comment: Interface-specific. Replace with content for your interface. -->

The ExDesc attribute configures a variety of run-time settings, two of which are included in every interface and are described in the following table.
    
**Note:** Keywords must be specified in upper case.

| Keyword | Description | Example |
|:-|:-|:-|
| PERFORMANCE_POINT=XX | When set, such point stores the amount of time, in seconds, that it takes an interface to complete a scan for a particular scan class. The lower the scan time, the better the performance.- <br><br>XX= interface ID | PERFORMANCE_POINT= 11 |
| TRIG or EVENT | For event-driven input points: each time the specified point changes, the SQL query is executed. If the point name contains spaces, you must enclose it in single quotes. If there are subsequent - parameters, you must specify a comma after the /EVENT specification. Valid conditions:<br><br>&bull; anychange <br>&bull; increment <br>&bull; decrement <br>&bull; nonzero<br><br>For details about defining - event- driven points, refer to the [PI Universal Interface (UniInt) User Guide](https://techsupport.osisoft.com/Downloads/All-Downloads/All-Groups/All-Products/All-Categories/Current-Version/uniint/). | /EVENT=sinusoid, … or<br><br>/EVENT =sinusoid anychange, … |

## ExtendedDescriptor Length

Depending on the version of the PI API and the PI Data Archive, this interface supports an ExDesc attribute whose length is at most 80 or 1023 characters. The following table indicates the maximum length of this attribute for all the different combinations of PI API and PI Data Archive versions.

| PI API | PI Data Archive | Maximum Length |
|:-|:-|:-|
| PI API | PI Data Archive | Maximum Length |
| 6.0.2 or later | 4.370.x or later | 1023 |
| 6.0.2 or later | Earlier than 3.4.370.x | 80 |
| Earlier than 1.6.0.2 | 4.370.x or later | 80 |
| Earlier than 1.6.0.2 | Earlier than 3.4.370.x | 80 |

## Performance Points

For UniInt-based interfaces, the extended descriptor is checked for the string PERFORMANCE_POINT. If this character string is found, UniInt treats this point as a performance point.
