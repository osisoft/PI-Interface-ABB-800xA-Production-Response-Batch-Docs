---
uid: IS_LossOfConnectivity
---


# Loss of connectivity to PI Interface for <interface name>

If the interface loses the ODBC connection to the RDBMS, it closes any prepared SQL statements. If it is still connected to the PI System, the interface writes I/O Timeout to its points (unless you disable this feature) and loops, trying once a minute to reconnect. If it succeeds in connecting to the RDBMS, it reissues the query that preceded the "dropped connection" error. You can configure the number of ODBC errors that triggers a reconnection: in PI ICU, on the **rdbodbc Optional Parameters** tab. The retry rate is not configurable.

For output tags, when the interface loses connectivity to the RDBMS, placeholder values are retained. The interface does not empty the update-event queue for output tags, so events might be lost if the queue overflows. To recover such lost events manually, set the recovery parameters (/OOO_OPTION) and restart the interface, so as to reprocess the period when the interface was disconnected from the RDBMS. For details about recovery, see Recovering historical data . For details about increasing the size of the event queue, see the PI Server documentation.
