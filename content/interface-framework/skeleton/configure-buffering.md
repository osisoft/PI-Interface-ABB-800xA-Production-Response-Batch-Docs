---
uid: SK_EnableBuffering
---

# Enable buffering

PI interfaces support PI Buffer Subsystem (PIbufSS), which you need to enable using PI ICU.

1. Stop the interface and open the **Tools > Buffering** option in PI ICU.

2. In **Buffer Manager**, click **Settings**.

3. In the Global pane, select On from the **Buffering** drop down to enable buffering with PI Buffer Subsystem.

4. Click **Save and Close**.

5. Start the buffering application and the interface.

6. Confirm that the interface works together with the buffering application by physically removing the connection between the interface computer and the PI Data Archive computer.
    
    **Note:** The DataSecurity attribute for interface points must permit write access for the buffering application's PI trust or mapping. The interface's PI trust does not require DataSecurity write permission.

7. Restart the interface computer and confirm that the interface and the buffering application restart.
