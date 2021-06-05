---
uid: LoggingAndErrorMessages
---

# Logging and error messages

The interface logs operational messages during interface startup, data collection and recovery. Additional messages are logged if you enable debugging. To view messages, open PI System Management Tools, go to **Operation** -- > **Message Logs** and click the **PI Message Log** tab. (From the command line, use the pigetmsg utility.)

For detailed information about interface logging, refer to the OSIsoft Knowledge Base article KB00401 - How to read new UniInt 4.5.0.x and later Interface message logs (now in PI Message Log, not PIPC.log).

For details about managing the error logging process, see the PI API Installation Instructions manual.

To enable debug output for troubleshooting, launch PI Event Frames Interface Manager, select your interface instance, and go to the **Operational Settings** tab.
