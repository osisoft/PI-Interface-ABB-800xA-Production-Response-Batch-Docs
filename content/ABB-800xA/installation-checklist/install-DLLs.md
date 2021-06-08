---
uid: InstallDLLsforABB800xA
---
# Install DLLs for ABB 800xA Production Response Batch

PI Interface for ABB 800xA Production Response Batch requires the installation of the the ABB Ability Manufacturing Operations Management (MOM) Process Intelligence SDK, which exposes the ABB 800xA Batch Production Response SDK DLLs that are required for the interface. After the DLLs are installed by the ABB Ability MOM Process Intelligence SDK, they must be copied to the batch interface executable directory.

1. Install the ABB Ability Manufacturing Operations Management (MOM) Process Intelligence SDK on the server where the interface is installed. Installing the SDK exposes DLL files that you need to install to make the interface work.

1. Copy the DLL files shown in the following table to the installation directory of the interface. Each DLL can be found in the Original File Location column of the table.

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

1. Using ABB's MOM utility, install the DLL files to the server on which the interface is installed, usually located at `%PIHome%\PIPC\Interfaces\ABB800xaPR`.
