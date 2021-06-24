---
uid: Scan
---

# Scan

By default, the Scan attribute has a value of 1, which means that scanning is turned on for the point. Setting the Scan attribute to 0 turns scanning off. If the Scan attribute is 0 when the interface starts, a message is written to the log and the point is not loaded by the interface. There is one exception to the previous statement.

If any PI point is removed from the interface while the interface is running (including setting the Scan attribute to 0), `SCAN OFF` will be written to the PI point regardless of the value of the Scan attribute. Two examples of actions that would remove a PI point from an interface are to change the point source or set the Scan attribute to 0. If an interface-specific attribute is changed that causes the point to be rejected by the interface, `SCAN OFF` will be written to the PI point.
