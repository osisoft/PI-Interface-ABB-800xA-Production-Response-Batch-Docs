---
uid: BIF_SourceTab
---

# Source tab

<!-- Mark Bishop 6/8/21: Topic customzied for ABB 800xA. Removed SQL language. -->

Configure the data sources that you want the interface to read. To add a data source, right-click the top **Sources** node and choose the **Add** option for the type of source you are configuring. 

**Note:** To use explicit logins for a local data store, ensure that the user running the interface and the user configuring the interface are the same user.

Using the Source template, configure the parameters as shown in this table:

<!-- Mark Bishop 6/8/21: Table is ABB 800xA specific -->

Parameter | Definition | Example configuration
--|--|--
USER | Required.<br><br>The user name required to explicitly login to ABB Ability MOM Services. Contact your ABB 800xA Administrator for additional guidance if needed. | `USER=abbuser`
PROTECTEDPASSWORD | Required.<br><br>The password for the user defined above. This will be encrypted by PI Event Frames Interface Manager. Contact your ABB 800xA Administrator for additional guidance if needed. | `PROTECTEDPASSWORD=Password`
CONNECTIONSTRING | Required.<br><br>The URL used to connect to ABB MOM Services. The encryption binding in the application server (such as WSS) and the hostname are used. Contact your ABB 800xA Administrator for additional guidance if needed. | `CONNECTIONSTRING=wss://hostname:10940/SDS`
IS95PRACCESSOR | Required.<br><br>ID of the IS95PRACCESSOR. This is typically set to "S95PR". Contact your ABB 800xA Administrator for additional guidance if needed. | `IS95PRACCESSOR=S95PR`
INCREMENTORID | Required.<br><br>ID of the Incrementor used to subscribe for any task information. This is not specific to any ABB setting, and can be completely defined by the interface administrator. | `INCREMENTORID=OSIInc`
DATASOURCE | Required.<br><br>Name of the Data Source. This is typically set to "PR_OL". Contact your ABB 800xA Administrator for additional guidance if needed. | `DATASOURCE=PR_OL`
ROWLIMIT | Required.<br><br>Maximum number of rows that should be returned at one time from ABB MOM Services. | `ROWLIMIT=1000 `
