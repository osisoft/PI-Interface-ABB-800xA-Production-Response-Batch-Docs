---
uid: BIF_ConfigureSecurityForPIAF
---

# Configure security for the PI Asset Framework

<!-- Static topic. No modifications usually required -->

To configure batch interface security settings for the PI Asset Framework, perform the following steps.

1. Launch PI System Explorer.

2. Click **Database** on the toolbar. The Select Database window opens, listing existing databases.

3. Right-click the database where you intend to store the batch event frames, and then click **Security**.

4. Browse to the category and enter the required settings:

    1. Set **Database** to read/write.
    2. Set **Categories** to read.
    3. Set **Element** to read/write.
    4. Set **Element templates** to read.
    5. Set **Event frames** to read/write.
