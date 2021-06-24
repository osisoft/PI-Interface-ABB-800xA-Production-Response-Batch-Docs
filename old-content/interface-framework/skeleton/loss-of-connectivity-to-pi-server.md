---
uid: SK_LossOfConnectivityToPIServer
---

# Loss of connectivity to PI Data Archive

If the interface loses its connection to the PI Server, it logs errors and continues running normally, attempting to restore the connection to the server. Without connection to the PI Data Archive, the interface will continue operating without issue. Data sent will either be lost or buffered if buffering is being used. If the interface restarts, without disconnected startup configured the interface will not be able to load PI points nor collect data until the connection to the PI Data Archive is restored.
