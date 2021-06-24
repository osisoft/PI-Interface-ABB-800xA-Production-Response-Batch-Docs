---
uid: SK_NameConventionsAndRequirements
---

# Name conventions and requirements

In the installation procedure below, it is assumed that the name of the interface executable is `<interfacename>.exe` and that the startup command file is called `<interfacename>.bat` (where you replace `<interfacename>` with the name of your actual interface).

## Configure the interface manually

It is customary for the user to rename the executable and the startup command file when multiple copies of the interface are run. For example, `<interfacename>1.exe` and `<interfacename1>1.bat` would typically be used for instance 1, `<interfacename>2.exe` and `<interfacename>2.BAT` for instance 2, and so on (where you replace `<interfacename>` with the name of your actual interface). When an interface is run as a service, the executable and the command file must have the same root name because the service looks for its command-line parameters in a file that has the same root name.
