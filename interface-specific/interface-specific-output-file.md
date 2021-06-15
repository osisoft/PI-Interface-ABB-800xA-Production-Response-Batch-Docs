---
uid: IS_InterfaceSpecificOutputFile
---

# Interface-specific output file for <interface name>

The file pointed to by the start-up parameter /OUTPUT= stores relevant operational information. During normal operation (/DEB=1) error logging is sufficient just to detect problems. A problem can then be drilled down with modified debug level. The amount of extra information depends on the debug level: /DEB=1-4.
    
**Note:** Errors related to tag values will also be reported in giving the tag a Bad Input or Bad Output state. This happens if the status of a RDBMS value is `BAD`
or the output operation failed. Points can also get a status of `I/O Timeout` if the interface detects connection problems.
