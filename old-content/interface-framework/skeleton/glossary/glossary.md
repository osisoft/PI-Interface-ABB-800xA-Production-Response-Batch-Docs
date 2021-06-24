---
uid: SK_Glossary
---

# Glossary 

## Available terms

The following are high-context terminologies used in this document.

* [Buffering](#buffering)
* [N-Way Buffering](#n-way-buffering)
* [ICU](#icu)
* [ICU Control](#icu-control)
* [Interface Node](#interface-node)
* [PI API](#pi-api)
* [PI Data Archive Collective](#pi-data-archive-collective)
* [PI Data Archive Node](#pi-data-archive-node)
* [PIHOME](#pihome)
* [PIHOME64](#pihome64)
* [PI Message Log](#pi-message-log)
* [PI SDK](#pi-sdk)
* [PI Server Node](#pi-server-node)
* [PI SMT](#pi-smt)
* [Pipc.log](#pipclog)
* [Point](#point)
* [Service](#service)
* [Tag (Input Tag and Output Tag)](#tag-input-tag-and-output-tag)

### Buffering
    
Buffering refers to an interface node's ability to store temporarily the data that interfaces collect and to forward these data to the appropriate PI Data Archives. 

### N-Way Buffering
    
If you have PI Data Archives that are part of a collective, PIBufss supports n-way buffering. N‑way buffering refers to the ability of a buffering application to send the same data to each of the PI Data Archives in a collective. (Bufserv also supports n-way buffering to multiple PI Data Archives in a collective; however, it does not guarantee identical archive records since point compression attributes could be different between PI Data Archives. With this in mind, OSIsoft recommends that you run PIBufss instead.) 

### ICU
    
ICU refers to the PI Interface Configuration Utility. The ICU is the primary application that you use to configure PI interface programs. You must install the ICU on the same computer on which an interface runs. A single copy of the ICU manages all of the interfaces on a particular computer. You can configure an interface by editing a startup command file. However, OSIsoft discourages this approach. Instead, OSIsoft strongly recommends that you use the ICU for interface management tasks.

### ICU Control

An ICU control is a plug-in to the ICU. Whereas the ICU handles functionality common to all interfaces, an ICU control implements interface-specific behavior. Most PI interfaces have an associated ICU control. 

### Interface Node

An interface node is a computer on which

* the PI API and/or PI SDK are installed, and
* PI Data Archive programs are not installed.

### PI API

The PI API is a library of functions that allow applications to communicate and exchange data with the PI Data Archive. All PI interfaces use the PI API. 

### PI Data Archive Collective

A PI Data Archive Collective is two or more replicated PI Data Archives that collect data concurrently. Collectives are part of the High Availability environment. When the primary PI Data Archive in a collective becomes 
unavailable, a secondary collective member node seamlessly continues to collect and provide data access to your PI clients. 

### PI Data Archive Node

A PI Data Archive node is a computer on which PI Data Archive programs are installed. The PI Data Archive runs on the PI Data Archive node. In earlier documentation, PI Data Archive was referred to as the PI Server. 

### PIHOME

PIHOME refers to the directory that is the common location for PI 32-bit client applications. A typical PIHOME on a 32-bit operating system is: C:\Program Files\PIPC. A typical PIHOME on a 64-bit operating system is: 
C:\Program Files (x86)\PIPC. PI 32-bit interfaces reside in a subdirectory of the Interfaces directory under PIHOME. For example, files for the 32-bit Modbus Ethernet Interface are in: [PIHOME ]\PIPC\Interfaces\ModbusE. This document uses [PIHOME ] as an abbreviation for the complete PIHOME or PIHOME64 directory path. For example, ICU files in: [PIHOME ]\ICU. 

### PIHOME64

PIHOME64 is found only on a 64-bit operating system and refers to the directory that is the common location for PI 64-bit client applications. A typical PIHOME64 is: C:\Program Files\PIPC. PI 64-bit interfaces reside in a 
subdirectory of the Interfaces directory under PIHOME64. For example, files for a 64-bit Modbus Ethernet Interface would be found in: C:\Program Files\PIPC\Interfaces\ModbusE. This document uses [ PIHOME ] as an abbreviation for the complete PIHOME or PIHOME64 directory path. For example, ICU files in: [ PIHOME ]\ICU. 

### PI Message Log

The PI message log is the file to which OSIsoft interfaces based on UniInt 4.5.0.x and later write informational, debug and error messages. When a PI interface runs, it writes to the local PI message log. This message file 
can only be viewed using the PIGetMsg utility. See the Message Logs section of the PI Universal Interface (UniInt) User Guide for more information on how to access these messages. 

### PI SDK

The PI SDK is a library of functions that allow applications to communicate and exchange data with the PI Data Archive. Some PI interfaces, in addition to using the PI API, require the use of the PI SDK. 

### PI Server Node

In earlier documentation, the term "PI Server" was used as a nickname for the PI Data Archive and a PI Server node was a computer on which PI Data Archive programs were installed. While the PI Data Archive remains a core 
server of the PI Server product, the product name "PI Server" now refers to much more than the PI Data Archive. OSIsoft documentation, including this user manual, is changing to use "PI Server" in this broader sense and "PI Data Archive" to refer to the historian core. 

### PI SMT

PI SMT refers to PI System Management Tools. PI SMT is the program that you use for configuring PI Data Archives. A single copy of PI SMT manages multiple PI Data Archives. PI SMT runs on either a PI Data Archive node or 
an interface node. 

### Pipc.log

The pipc.log file is the file to which OSIsoft interfaces based on UniInt versions earlier than 4.5.0.x write informational and error messages. When a PI interface runs, it writes to the pipc.log file. The ICU allows easy 
access to the pipc.log. 

### Point

The PI point is the basic building block for controlling data flow to and from the PI Data Archive. For a given timestamp, a PI point holds a single value. A PI point does not necessarily correspond to a "point" on the 
data source device. For example, a single "point" on the data source device can consist of a set point, a process value, an alarm limit, and a discrete value. These four pieces of information require four separate PI points. 

### Service

A Service is a Windows program that runs without user interaction. A service continues to run after you have logged off from Windows. It has the ability to start up when the computer itself starts up. The ICU allows you to 
configure a PI interface to run as a service. 

### Tag (Input Tag and Output Tag)

The Tag attribute of a PI point is the name of the PI point. There is a one-to-one correspondence between the name of a point and the point itself. Because of this relationship, PI System documentation uses the terms "tag" 
and "point" interchangeably. Interfaces read values from a device and write these values to an input tag. Interfaces use an output tag to write a value to the device. 
