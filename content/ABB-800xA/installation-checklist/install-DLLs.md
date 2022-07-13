---
uid: InstallDLLsforABB800xA
---
# Install DLLs

PI Interface for ABB 800xA Production Response Batch requires the installation of the ABB Ability Manufacturing Operations Management (MOM) Process Intelligence SDK, which exposes the ABB 800xA Batch Production Response SDK DLLs that are required for the interface. After the DLLs are installed by the ABB Ability MOM Process Intelligence SDK, they must be copied to the batch interface executable directory.

1. Install the ABB Ability Manufacturing Operations Management (MOM) Process Intelligence SDK on a server. It is not a requirement that you install the SDK in the same location where you installed the interface. It must be in a location where the interface can connect to it. Installing the SDK exposes DLL files that you need to install to make the interface work.

1. Copy the following DLL files to the installation directory for the interface. To do this, locate the DLL file in your original file location and then place it in the folder where you installed the interface (%ProgramFiles(x86)%\pipc\interfaces\ABB800xaPR). 

    | DLL File | Original File Location |
    |--|--|
    | ABB.SDS.Desktop.dll | `<Installation Directory>\Program Files\ABB\SDS\Server\Apps\Configurator\desktop` |
    | ABB.SDS.Server.Client.dll | `<Installation Directory>\Program Files\ABB\SDS\Server\Apps\Configurator\desktop` |
    | ABB.SDS.dll | `<Installation Directory>\Program Files\ABB\SDS\Server` |
    | Castle.Core.dll | `<Installation Directory>\Program Files\ABB\SDS\Server` |
    | Newtonsoft.Json.dll | `<Installation Directory>\Program Files\ABB\SDS\Server` |
    | VtrinLib.dll | `<Installation Directory>\Program Files\ABB\SDS\Server` |
    | ABB.SDS.S95PR.Accessor.dll | `%ProgramData%\ABB\SDS\Server\Apps\ABB.SDS.S95PR.Accessor.Server\Server` |
    | ABB.SDS.Server.Accessors.dll | `%ProgramData%\ABB\SDS\Server\Apps\ABB.SDS.Batch.Accessors.Server\server` |
    | ABB.SDS.Server.Accessors.Interfaces.dll | `%ProgramData%\ABB\SDS\Server\Apps\ABB.SDS.Batch.Accessors.Server\server` |

