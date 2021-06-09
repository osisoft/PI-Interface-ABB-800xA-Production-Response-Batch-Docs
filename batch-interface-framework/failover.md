---
uid: Failover
---

# Failover 

OSIsoft's batch interfaces and PI Event Frames Generator support two types of failover: 

## Interface failover 

OSIsoft supports multiple instantiations of batch interfaces. If one fails, a second takes over the data collection process. For details on configuring failover, see [Configure failover](xref:BIF_ConfigureInstancesForFailover).

## Server failover 
   
If a server fails, batch data collection stops but failover on PI AF continues to work through a backup server. If server failover occurs while event frames are being generated, data is transferred to both primary and secondary servers. 
