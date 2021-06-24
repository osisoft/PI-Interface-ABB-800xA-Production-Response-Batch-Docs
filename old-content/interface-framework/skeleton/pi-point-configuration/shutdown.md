---
uid: SK_Shutdown
---

# Shutdown 

The Shutdown attribute is 1 (true) by default. The default behavior of the PI Shutdown Subsystem is to write the SHUTDOWN digital state to all PI points when PI is started. The timestamp that is used for the SHUTDOWN events is retrieved from a file that is updated by the Snapshot Subsystem. The timestamp is usually updated every 15 minutes, which means that the timestamp for the SHUTDOWN events will be accurate to within 15 minutes in the event of a power failure. For additional information on shutdown events, refer to PI Data Archive manuals.
    
**Note:** The SHUTDOWN events that are written by the PI Shutdown Subsystem are independent of the SHUTDOWN events that are written by the interface when the following command-line parameter is specified: `/stopstat=Shutdown`

SHUTDOWN events can be disabled from being written to PI points when the PI Data Archive is restarted by setting the Shutdown attribute to 0 for each point. Alternatively, the default behavior of the PI Shutdown Subsystem can be changed to write SHUTDOWN events only for PI points that have their Shutdown attribute set to 0. To change the default behavior, edit the Shutdown.dat file, as discussed in the PI Data Archive manuals.

## Bufserv and PIBufss

It is undesirable to write shutdown events when buffering is being used. Bufserv and PIBufss are utility programs that provide the capability to store and forward events to a PI Data Archive, allowing continuous data collection when the PI Data Archive is down for maintenance, upgrades, backups and unexpected failures. That is, when the PI Data Archive is shutdown, Bufserv or PIBufss will continue to collect data for the interface, making it undesirable to write SHUTDOWN events to the PI points for this interface. Disabling Shutdown is recommended when sending data to a Highly Available PI Data Archive collective. Refer to the Bufserv or PIBufss manuals for additional information.
