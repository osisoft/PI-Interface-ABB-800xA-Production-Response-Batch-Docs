---
uid: SK_InterfaceDirectories
---

# Interface directories

All PI interface installations use a standardized directory structure as described below:

## PIHOME directory tree

### 32-bit Interfaces

The [PIHOME] directory tree is defined by the PIHOME entry in the  `pipc.ini` configuration file. This  `pipc.ini` file is an ASCII text file, which is located in the `%windir% `directory.
For 32-bit operating systems, a typical  `pipc.ini` file contains the following lines:

```text
[PIPC]
PIHOME=C:\Program Files\PIPC
```

For 64-bit operating systems, a typical  `pipc.ini` file contains the following lines:

```text
[PIPC]
PIHOME=C:\Program Files(X86)\PIPC
```

The above lines define the root of the PIHOME directory on the C: drive. The PIHOME directory does not need to be on the C: drive. OSIsoft recommends using the paths shown above as the root PIHOME directory name.
    
**Note:** Restrict the Windows accounts that can create or write files in the ` %PIHOME% ` folder and subfolders.

## PIHOME64 directory tree

### 64-bit interfaces

The [PIHOME64] directory tree is defined by a System Environmental Variable called PIHOME64.

A typical value for this environmental variable is `C:\Program Files\PIPC\`.

The above lines define the `\Program Files\PIPC` directory as the root of the PIHOME64 directory tree on the C: drive. OSIsoft recommends using `\Program Files\PIPC` as the root directory name. The PIHOME64 directory does not need to be on the C: drive.
    
**Note:** Restrict the Windows accounts that can create or write files in the` %PIHOME% `folder and subfolders.

## Interface installation directory

The installation kit for the read/write version will automatically install the interface to: `PIHOME\Interfaces\<interfacename>` (where `<interfacename>` is the name of your actual interface).
    
**Note:** PIHOME is defined in the  `pipc.ini` file.
