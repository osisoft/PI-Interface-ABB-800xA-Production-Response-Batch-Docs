---
uid: IS_SQLExamples
---

# SQL examples for PI Interface for <interface name>

<!-- Draft comment: Interface-specific topic. REPLACE WITH CONTENT FOR YOUR INTERFACE. -->

The example suite below shows various approaches for transferring data between the PI Data Archive and an RDBMS. Examples are illustrative and are not installed as part of the interface. To implement the examples:

1. Store the SQL queries in a text file in a directory that is configured for SQL files on the **PI ICUrdbodbc > Startup Parameters tab**; alternatively, define the SQL queries in the ExtendedDescriptor of a PI tag.

2. Create the PI points, setting the example-specific attributes as described in the example.

3. For all points in these examples, the following settings apply:

    | Point Attribute | Description |
    |:-|:-|
    | Location1 | Interface instance ID |
    | Location2 | 0: Processes only the first row 1: Processes all rows |
    | Location3 | Data distribution strategy:<br><br>&bull; 0: Single <br>&bull; -1: Tag Distribution <br>&bull; -2: RxC (Row x Column) |
    | Location4 | Scan class number |
    | Location5 | &bull; 0: Exception reporting is enabled <br>&bull; 1: Exception reporting is turned off <br>&bull; 2: Add events @ the same timestamp <br>&bull; 3: For tag distribution and RxC - process only - newer data |
    | InstrumentTag | Name of the query file |
    | PointSource | Matches point source configured for interface instance |
    | SourcePoint | For output tags - name of the tag that triggers the execution if its snapshot value changed |

4. Create the RDBMS table as specified and populate the table with sample data. In the examples, note that the name of the SQL query files, RDBMS tables, and table column names is up to you.
    
    **Note:** In some examples, the semantic meaning of columns in the SELECT list is predetermined and the interface assumes the first column is a timestamp, second is a value, and third is status. If every column in the SELECT list is aliased using the set of the "PI_" keywords, the meaning of individual columns is determined according to these keywords.
    