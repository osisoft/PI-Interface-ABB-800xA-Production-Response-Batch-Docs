---
uid: SK_ReadOnlyAndWriteOnlyInterfaces
---

# Read-only and read-write interfaces

OSIsoft provides both read-only and read-write options of many interfaces. Due to the inherent security risks associated with writing to the data source, OSIsoft recommends using the read- only option when possible.

* If you do not need to write to the data source, select the read-only version of the interface. For more information about the read-only version of the interface, or if you are migrating from a read-write version to a read-only version and want to view the migration procedure, refer to the [Read-only versus read-write FAQ](https://livelibrary.osisoft.com/LiveLibrary/content/en/int-read-faq-v1/GUID-9F207C13-40E4-472E-8D40-8D6EE87C86F7). If a read-only version is not available, disable interface updates to the data source. For more information, refer to <xref:SK_DisableReadWriteUpdatesToTheDataSource>.

* If you need to write to the data source, select the read-write version of the interface and secure your points in the following ways:

  * Create an output point whitelist file that is secured so that only authorized users can change it. For more information, refer to the [PI Universal Interface (UniInt) Framework User Guide](https://livelibrary.osisoft.com/LiveLibrary/web/pub.xql?action=publist_home&pub_category=PI-Universal-Interface-(UniInt)-Framework).
  
  * Isolate output points using a separate interface instance from the input point interface instance.
