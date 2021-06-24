---
uid: SK_BaseObjectOverview
---

# BaseObject overview

In the OCS configuration, the BaseObject is a critical parameter that specifies the OCS collection into which OMF Health streams are stored.

Examples, from the config file samples provided in this user guide:

* `BaseObject=MyBaseObjectForURL`
* `BaseObject=/api/v1`

The BaseObject includes the version number (v1 in the example above) of the OCS api that is running.
    
**Note:** It may become necessary to change the BaseObject if OCS stops supporting a specific version of `OMF Health Messaging`.
