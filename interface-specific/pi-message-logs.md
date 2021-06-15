---
uid: IS_PIMessageLogs
---

# PI message logs for <interface name>

<!-- Draft comment: This is an interface-specific topic. REPLACE WITH INFORMATION SPECIFIC TO YOUR INTERFACE. -->

The location of the message log depends upon the platform on which the interface is running.

For more information about logs for interfaces running on Windows, see REF UniIntMessageLogging \* MERGEFORMAT UniInt Interface Message Logging for UniInt 4.5.0.x and later Interfaces or [KB00401](https://techsupport.osisoft.com/Troubleshooting/KB/KB00401) on the OSIsoft technical support web site.

Messages are written to the log file at the following times.

* When the interface starts, many informational messages are written to the log. These messages include the version of the interface, the version of UniInt, the command-line parameters used, a the number of points.

* As the interface loads points, messages are sent to the log if there are any problems with the configuration of the points.

* If the UniInt /dbUniInt parameter is found in the command-line, then various informational messages are written to the log file.
