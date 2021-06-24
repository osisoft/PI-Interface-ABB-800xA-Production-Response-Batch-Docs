---
uid: BIF_PIServerConnectivity
---

# PI server connectivity

<!-- Static topic. No modifications usually required -->

If a connection is lost during processing, the interface suspends all actions until it reconnects to the PI Data server or the data source. If the data source connection is down, the interface tries to reconnect on every scan until it succeeds. If the PI Data server connection is lost, the interface attempts to reconnect periodically until it times out.

You can configure both the retry interval and the timeout period on the **Time Settings** tab of the PI Event Frames Interface Manager. The interface logs any connection errors that occur.
