---
uid: SK_InstallationInstructions
---

# Installation instructions

OSIsoft recommends that interfaces be installed on interface computers instead of directly on the  **PI Data Archive** computer. An interface computers is any computer other than the  **PI Data Archive** computer where the PI Application Programming Interface (PI API) is installed (see the PI API manual). With this approach, the  **PI Data Archive** need not compete with interfaces for the machine's resources. The primary function of the  **PI Data Archive** is to archive data and to service clients that request data.

After the interface has been installed and tested, buffering should be enabled on the interface computer. Buffering refers to either PI API Buffer Server (Bufserv) or the PI Buffer Subsystem (PIBufss).

In most cases, interfaces on interface computer should be installed as automatic services. Services keep running after the user logs off. Automatic services automatically restart when the computer is restarted, which is useful in the event of a power failure.

The guidelines are different if an interface is installed on the  **PI Data Archive** computer. In this case, the typical procedure is to install the  **PI Data Archive** as an automatic service and install the interface as an automatic service that depends on the PI Update Manager and PI Network Manager services.
    
**Note:** By default, buffering is not enabled on the  **PI Data Archive** computer. Bufserv or PIBufss can be enabled on the  **PI Data Archive** computer so that interfaces on the  **PI Data Archive** computer do not need to be started and stopped in conjunction with the  **PI Data Archive**.

[!include[catalog files](../../includes/catalog-files.md)]
