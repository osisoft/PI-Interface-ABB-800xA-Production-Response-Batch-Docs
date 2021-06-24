---
uid: SK_VerifyInterfaceStartup
---

# Verify interface startup

You can use the message log to check for proper startup of the interface.

1. Display the message log. To do this, open PI System Management Tools and click **Operation > Message Logs**.

2. Start the interface. To do this, open PI ICU, navigate to the interface instance, and then click **Interface > Start Interactive**.

    PI ICU opens a command window and runs the startup batch (`.bat`) file. The interface logs messages as it attempts to initialize and run.

3. View the log to identify messages indicating success or errors.

4. To stop the interface, close the command window.
