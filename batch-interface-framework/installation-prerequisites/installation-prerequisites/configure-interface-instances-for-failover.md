---
uid: BIF_ConfigureInstancesForFailover
---

# Configure interface instances for failover

To ensure that batch data continues to be collected if an instance of the interface fails, you can configure multiple interface instances to run in failover mode. The instances must be configured identically.

To enable failover, perform the following steps before you start the interface instances:

1. Configure instances of the interface on different host computers. Assign the same interface ID and point source, and assign unique failover IDs to each instance. 
    
    You can configure more than two instances for failover.
    
2. In the target PI Data Archive, create a string tag and configure it with the same point source and Location1 (interface ID) as the interfaces.

    The interface instance uses this string tag to coordinate failover.  
    
3. Using PI Event Frame Interface Manager, go to the **Operational Settings** tab and configure the failover settings.                                                    

    * **Failover tag**
  
        The name of the tag that you created in the previous step.
    
    * **Failover identifier**
    
        A unique ID for the interface instance.
    
    * **Failover swap time**
        
        The amount of time that the current primary interface must be unavailable before failover occurs.

4. Start the interface instances.

    When the primary interface instance is operational, it updates the failover tag with the timestamp of the last value written. The backup instance monitors this tag and, if the failover swap time elapses and the failover tag has not been updated, the backup instance takes over data collection and becomes the primary instance.
