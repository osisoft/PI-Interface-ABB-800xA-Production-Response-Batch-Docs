---
uid: IS_SupportedFeatures
---

# Supported features for PI Interface for <interface name>

<!-- Draft comment: INTERFACE-SPECIFIC: Enter content for your interface. -->

The following table describes features that this interface supports. Some features are described in more detail after the table.

| Feature | Support |
|:-|:-|
| Auto Creates PI Points | No |
| Point Builder Utility | No |
| ICU Control | Yes |
| PI Point Types | Float16 / Float32 / Float64 / Int16 / Int32 / Digital / String / Timestamp |
| Sub-second Time stamps | Yes |
| Sub-second Scan Classes | Yes |
| Automatically Incorporates PIPoint Attribute Changes | Yes |
| Exception Reporting | Yes |
| Outputs from PI Data Archive | Yes (event-based and scan-based) |
| <sup>1</sup> Read only interface available | No |
| Inputs to PI Data Archive | Scan-based, unsolicited, and event points |
| <sup>1</sup> Questionable Bit Support | Yes |
| <sup>1</sup> PI Annotations Support | Yes |
| Multi-character PointSource | Yes |
| Maximum Point Count | Unlimited |
| Required PI API Version | 1.6.0+ |
| <sup>1</sup> Uses PI SDK | Yes ( to access annotations and some point attributes) |
| PINet String Support | No |
| <sup>1</sup> Source of Timestamps | RDBMS or PI Server, depending on how you define the query that updates the target. |
| <sup>1</sup> History Recovery | Yes |
| <sup>1</sup> UniInt-based | Yes |
| <sup>1</sup> Disconnected Startup | No |
| <sup>1</sup> SetDeviceStatus | Yes |
| <sup>1</sup> Failover | Interface level failover: UniInt Phase 2 Failover (cold)<br>Server level failover: RDBMS Server-level failover for mirrored Microsoft SQL Servers only |
| <sup>1</sup> Vendor Software Required on PI Interface Node / PINet Node | Yes |
| Vendor Software Required on Foreign Device | Yes |
| Vendor Hardware Required | No |
| Additional PI Software Included with Interface | No |
| <sup>1</sup> Device Point Types | See note below. |
| Serial-Based Interface | No |

<sup>1</sup>  See paragraphs below for further explanation.

## Platforms

The interface is designed to run on the above mentioned Microsoft Windows operating systems and their associated service packs. Please contact OSIsoft Technical Support for more information. 

## Read-only Interface available

A read-only version of this interface is NOT available because it does not implement any logic that would prevent users to specify SQL statements that could write to RDBMS. In order to enforce read only access to a database a user with read only privileges should be configured and used.
        
**Note:** As a security best practice, OSIsoft recommends creating a database user with read only privileges and reference it through the /User_ODBC start-up parameter.

## Support for reading/writing to PI Questionable Flag and Annotation

Next to the timestamp, value, and status, the RDBMSPI interface can write/read also to/from PI questionable flag and annotation. 

## Uses PI SDK

This Interface specifically makes PI SDK calls to access some of the PI Point attributes and read and write PI annotations. 

## Source of Time stamps

The interface can accept time stamps from the RDBMS or it can provide PI Server synchronized time stamps. 

## History Recovery

For output tags, the interface goes back in time and uses values stored in the PI Archive for outputting them through configured SQL statements (mostly INSERTs or UPDATEs). 

For input tags, history recovery often depends on the WHERE condition of a SELECT query. Moreover, the interface allows for chunking longer recovery intervals so that the memory is not taxed during the initial query. 

## UniInt-based

UniInt stands for Universal Interface. UniInt is not a separate product or file; it is an OSIsoft‑developed template used by developers and is integrated into many interfaces, including this interface. The purpose of UniInt is to keep a consistent feature set and behavior across as many of OSIsoft's interfaces as possible. It also allows for the very rapid development of new interfaces. In any UniInt-based interface, the interface uses some of the UniInt-supplied configuration parameters and some interface-specific parameters. UniInt is constantly being upgraded with new options and features. The [PI Universal Interface (UniInt) User Guide](https://techsupport.osisoft.com/Downloads/All-Downloads/All-Groups/All-Products/All-Categories/Current-Version/uniint/) is a supplement to this manual. 

## SetDeviceStatus

The RDBMSPI Interface is built with health tags support. The following events will be written into the tag, which has in ExDesc =[UI_DEVSTAT] keyword defined.

| Keyword | Description |
|:-|:-|
| `"0 | Good | "` | The interface is properly communicating and gets data from/to the RDBMS system via the given ODBC driver |
| `"3 | 1 device(s) in error | "` | ODBC data source communication failure |
| `"4 | Intf Shutdown | "` | The interface was shut down |
   
**Note:** Refer to the [PI Universal Interface (UniInt) User Guide](https://techsupport.osisoft.com/Downloads/All-Downloads/All-Groups/All-Products/All-Categories/Current-Version/uniint/) for more information on how to configure health points.

## Failover

* UniInt Failover Support

    This interface supports UniInt Phase 2, cold failover.

    * This failover solution requires that two copies of the interface be installed on different interface nodes with one instance being active and the second in a passive mode. Phase 2 Failover also requires each interface have access to a shared data file. Failover operation is automatic and operates with no user interaction. Each interface participating in failover has the ability to monitor and determine liveliness and failover status. To assist in administering system operations, the ability to manually trigger failover to a desired interface is also supported by the failover scheme. The failover scheme is described in detail in the UniInt Interface User Manual, which is a supplement to this manual.

* Server-Level Failover

The interface supports the FAILOVER_PARTNER keyword in the connection string when used with Microsoft SQL Server 2005 (and above) and the Native Client ODBC driver. In other words, in case the interface connects to the mirrored Microsoft SQL Servers and the connection gets broken, the interface will attempt to reconnect to the second SQL Server.

## Vendor Software Required

The RDBMS specific ODBC driver must be installed and configured on the interface node. 

## Device Point Types

For full description of the ODBC supported data types see the [ODBC Programmer's Reference](http://msdn.microsoft.com/en-us/library/ms714177.aspx). The interface does some internal consideration in terms of mapping the RDBMS data types to PI data types and vice versa. 
