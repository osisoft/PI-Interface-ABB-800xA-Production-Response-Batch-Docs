---
uid: SK_ExcMaxExcMinAndExcDev
---

# ExcMax ExcMin and ExcDev (exception processing)

Exception reporting enables you to capture the minimum amount of data required to meaningfully represent a trend. The following parameters configure exception reporting in the PI interface.

* ExcMax: The maximum time period allowed between sending values to the PI Data Archive.
* ExcMin: The minimum time period between values sent to the PI Data Archive.
* ExcDev: The minimum change from the last value sent to the PI Data Archive required for the interface to send a new value.

Exception processing is not performed for queries that include PI annotations: all data retrieved by such queries is archived.

To further filter the amount of data that is captured, you can configure a tag's compression settings so that only meaningful deviations are archived. For more information about exception processing and compression, see the [PI Universal Interface (UniInt) Framework User Guide](https://livelibrary.osisoft.com/LiveLibrary/web/pub.xql?action=publist_home&pub_category=PI-Universal-Interface-(UniInt)-Framework).
