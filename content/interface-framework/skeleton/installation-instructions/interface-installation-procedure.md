---
uid: SK_InterfaceInstallationProcedure
---

# Interface installation procedure

The interface setup program uses the services of the Microsoft Windows Installer. Windows Installer is a standard part of Windows operating systems. To install, run the appropriate installation kit.

* 32-bit Interface: `<interfacename>_#.#.#.#_.exe`
* 64-bit Interface: `<interfacename>_#.#.#.#_x64_.exe`

## Silent installation procedure

To launch a silent installation, type: `Setup.exe -f silent.ini`

The `silent.ini` file is included in the interface installation kit. You can make site-specific alterations to the file as needed. See the `silent.ini` file for further information and descriptions of available arguments.
    
**Note:** All other modules in the interface installation kit are configured to be installed by default.
