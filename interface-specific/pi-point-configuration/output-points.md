---
uid: IS_OutputPoints
---

# Output Points

<!-- Draft comment: SHARED SKELETON TOPIC: DO NOT EDIT. OMIT THIS TOPIC IF YOUR INTERFACE DOES NOT SUPPORT OUTPUT POINTS -->

Output points control the flow of data from the PI Data Archive to any destination that is external to the PI Data Archive, such as a PLC or a third-party database. For example, to write a value to a register in a PLC, use an output point. Each interface has its own rules for determining whether a given point is an input point or an output point. There is no particular PI point attribute that distinguishes a point as an input point or an output point.
    
**Note:** If outputs to the data source device are not needed, specify a database user with read-only privileges and reference it through the /User_ODBC start-up parameter. Alternatively, implement an explicit output point whitelist, which provides a defense against accidental or malicious changes to a database.
