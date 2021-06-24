---
uid: IS_PrinciplesOfOperation
---

# Principles of operation for PI Interface for <interface name>

<!-- Draft comment: This is an interface-specific topic. REPLACE WITH INFORMATION SPECIFIC TO YOUR INTERFACE. -->

To read data from an RDBMS into the PI Data Archive, you define input tags, which are associated with SELECT queries that return columns containing values for the following tag attributes:

* Timestamp
* Value
* Status
* Questionable (optional)
* Annotation (optional)

To write data from the PI Data Archive to the RDBMS, you define output tags, which are associated with INSERT , UPDATE or DELETE queries.

Queries can contain placeholders for replaceable parameters. Placeholders are evaluated when the query is executed.

For efficiency in reading data from the RDBMS and writing it to the PI Data Archive, the interface supports several distribution strategies, depending on the structure of the result rows returned by the SELECT query:

* One PI point value per row: Each row returned in the result set returned by the SELECT query contains a single timestamp, value, status and (optionally) questionable and/or annotation, but no PI tag name.

* Multiple PI point values per row (the "tag group" approach): Each row in the result set contains values for more than one PI point. To associate a specific column with a PI point, you specify the column position in the Location3 point attribute.

* Read the PI point name from the row: To handle result sets that include rows for multiple PI points, the interface provides the "tag distribution" and "RxC" (row by column) distribution approaches, depending on whether the row includes one value for one tag or values for multiple tags.

Tags can be scanned or event-driven. Scanned tags are read or written at a regular interval that is defined by the scan class assigned to the tag. Event-driven tags are read or written when a specified trigger tag is updated. The interface provides several options for handling data that does not arrive in timestamp sequence (out-of-order data).

Besides collecting data in real time, the interface can recover historical data from the PI Data Archive to an RDBMS, or from the RDBMS to the PI Data Archive. You can configure the period to be restored, and after recovery is complete, the interface can either exit or begin collecting real- time data.

The interface runs on Windows either as a console application or Windows service. It uses ODBC to connect to the RDBMS. For the ODBC connection, you define the data source name (DSN) using the **Data Sources (ODBC)** Windows control panel and configure the interface instance to connect to the database using the DSN. The following figure illustrates a typical configuration, with the PI Server, RDBMS and interface running on different nodes.

![alt](https://link)

## Loss of connectivity to RDBMS

If the interface loses the ODBC connection to the RDBMS, it closes any prepared SQL statements. If it is still connected to the PI System, the interface writes I/O Timeout to its points (unless you disable this feature) and loops, trying once a minute to reconnect. If it succeeds in connecting to the RDBMS, it reissues the query that preceded the "dropped connection" error. You can configure the number of ODBC errors that triggers a re-connection: in PI ICU, on the **rdbodbc > Optional Parameters** tab. The retry rate is not configurable.

For output tags, when the interface loses connectivity to the RDBMS, placeholder values are retained. The interface does not empty the update-event queue for output tags, so events might be lost if the queue overflows. To recover such lost events manually, set the recovery parameters (/OOO_OPTION ) and restart the interface, so as to reprocess the period when the interface was disconnected from the RDBMS. For details about increasing the size of the event queue, see the [PI Server documentation](https://livelibrary.osisoft.com/LiveLibrary/web/ui.xql?action=html&resource=publist_home.html&pub_category=PI-Server).

## Loss of connectivity to PI Server

If the interface loses its connection to the PI Server, it logs errors and continues running normally, attempting to restore the connection to the server. While the interface is disconnected from the PI Server, it cannot read values for the snapshot placeholders (TS,VL, SS_I, etc.) and the attribute placeholders (`AT.xxx`), which are used to specify values for replaceable parameters in SQL queries. If buffering is enabled, queries without placeholders continue collecting data, and queries with placeholders report an error.
