---
uid: BIF_InitializationFileReference
---

# Initialization file reference

<!-- Customized for ABB 800xA. -->

The initialization (.ini) file stores configuration information for an interface instance. The PI Event Frame Interface Manager configuration tool generates and updates this file each time you edit the instance configuration. You can access initialization files from [!include[programdata](../includes/dir-long.md)]. 

**Note:** Before release 4.x, initialization files were stored in the interface installation directory.

**Tip:** To ensure a valid .ini file, use the PI Event Frame Interface Manager configuration tool. Do not edit the .ini file manually.

Use this appendix to learn about the contents of the .ini file for troubleshooting purposes.

The .ini file contains the following sections:

* **COMMAND LINE PARAMETERS:** Defines basic interface settings.
* **SIMPLE SWITCHES:** Defines connection settings.
* **[SOURCE TEMPLATE](source-template.md):** Defines the settings required to connect to the data source and events to be skipped (filtered).
* **[RECIPE TEMPLATE](recipe-templates.md):** Defines how data is recorded at each level of the batch hierarchy.
* **[TAG TEMPLATE](tag-templates.md):** Defines how tags are created and updated based on incoming data from the data source.
* **[PROPERTY TEMPLATE](property-templates.md):** Define how PI properties or event frame attributes are created based on incoming data from the data source.
* **[TRANSLATIONS](translation-templates.md):** Maps text from the data source language to the target language for the PI System.
* **DCS LINK TEMPLATE:** Define rules for linking event frames created by different interfaces.

In defining settings for templates, you can use the following wildcards to compose expressions:

| Wildcard | Description |
| -------- | ----------- |
| # | single digit numerical value (0-9) |
| @ | single alphabetic character (a-z, A-Z) |
| ? | any single character |
| ! | repeat previous mask symbol |
| * | any number of characters |

