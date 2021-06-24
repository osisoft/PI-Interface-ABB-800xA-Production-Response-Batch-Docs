---
uid: SK_MultipleEndpointConfiguration
---

# Multiple EndPoint configuration

Multiple endpoints may be configured for the interface. Here is an example of a config file with multiple endpoints configured:

```text
EndPointType=OCS
URL=MyExampleURL1.example.com
Port=443
BaseObject=/api/v1-example1
TenantID=abc12345-d6e7-8f9a-1b2c34567891
Namespace=Example1
IdentityProviderURL=/identity/connect/token
ClientID=12345abc-de67-8910-11f1-ab21c35478a98
ClientSecret=xBqgOD6fbWmfZt4XIfcprxdjsj845ey/X498WA8897k= 

EndPointType=OCS
URL=MyExampleURL2.example.com
Port=443 BaseObject=/api/v1-example2
TenantID=def15987-d7f8-8d9b-1c4e38468716
Namespace=Example2
IdentityProviderURL=/identity/connect/token
ClientID=89641cde-fa79-8645-45f9-cd34f98467a63
ClientSecret=yDaq1D6fbWmfZt4XIdkapeufij845ey/Z987NE5467P=

EndPointType=PIWebAPI
HostName=FactoryPiServer1
Port=443
User=FactoryDomain\PI_Admin_User
Password=123Password###!

EndPointType=PIWebAPI
HostName=EnterprisePiServer1
Port=443
User=EnterpriseDomain\PI_Admin_User
Password=456Password@@@!
```
