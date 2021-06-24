---
uid: IS_CommandLineParameters
---

# Command line parameters

<!-- Draft comment: This is an interface-specific topic. REPLACE WITH CONTENT FOR YOUR INTERFACE. -->

## Sample RDBMSPI.bat fSile

The following table lists the interface-specific command line parameters used in the interface startup batch file to configure settings. These parameters are provided for debugging purposes to help you read the file. 

To ensure a correctly-formatted file, use the PI Interface Configuration Utility to configure the interface.

In addition to interface specific parameters, all UniInt interfaces support a common set of parameters. For details, refer to the [PI Universal Interface (UniInt) User Guide](https://techsupport.osisoft.com/Downloads/All-Downloads/All-Groups/All-Products/All-Categories/Current-Version/uniint/).

| Parameter | Description |
|:-|:-|
| `/BAD1= #`<br>Default: 0 (Optional) | The beginning of the range in the system digital state table that contains Bad Input status strings. |
| `/BAD2= #`<br>Default: 0 (Optional) | The end of the range in the system digital state table that contains Bad Input status strings. |

The following is an example file:

```text
REM ==========================================================================
REM
REM RDBMSPI.BAT
REM 
REM Sample startup file for the Relational Database (RDBMS via ODBC) Interface
REM 
REM =========================================================================== 
REM
REM OSIsoft recommends using PI ICU to modify startup files.
REM
REM Sample command line
REM 
RDBMSPI.exe
/ps=RDBMSPI ^
/id=1 ^
/DSN=Oracle11 ^
/User_ODBC=system ^
/host=XXXXXX:5450 ^
/f=00:00:05 ^
/f=00:00:10 ^
/f=00:00:15 ^
/Output="C:\Program Files\PIPC\Interfaces\RDBMSPI\Log\RDBMSPI.out" ^
/SQL="C:\Program Files\PIPC\Interfaces\RDBMSPI\SQL\" ^
/DEB=1 ^
/PISDK=1 ^
/Recovery=TS ^
/Recovery_Time=*-5m
REM
REM End of RDBMSPI.bat
```
