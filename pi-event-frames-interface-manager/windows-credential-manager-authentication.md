---
uid: BIF_WindowsCredentialManagerAuthentication
---

# Windows Credential Manager for authentication

As a security best practice, [!include[interface](../includes/product-short.md)] stores any credentials that you enter during interface configuration to Windows Credential Manager. [!include[interface](../includes/product-short.md)] uses these credentials to authenticate with: 

* PI Data server 
* PI Asset Framework
* The batch interface data source

Storage of credentials within Windows Credential Manager benefits you by:

* Caching credentials for future authentication, so that you do not have to re-enter them.
* Removing any reference to passwords within the interface instance .ini file.
* Encrypting the credentials.

**Tip:** For more information on where to configure credentials that [!include[interface](../includes/product-short.md)] uses for authentication, see:

* <xref:BIF_ServerInformationTab>
* <xref:BIF_SourceTab>

## Credential creation

When you configure an interface using the PI Event Frames Interface Manager (see links in tip above), [!include[interface](../includes/product-short.md)] temporarily writes the credentials that you enter to the applicable .ini file. These settings remain in the .ini file until you start the interface. 

After you start [!include[interface](../includes/product-short.md)], it makes the following updates:

* All credentials are saved to Windows Credential Manager.
* Within the interface .ini file, any reference to passwords are removed.

## Credential storage

After you start [!include[interface](../includes/product-short.md)], the credentials that it uses for authentication with PI components and data sources are listed in [Windows Credential Manager](https://support.microsoft.com/en-us/windows/accessing-credential-manager-1b5c916a-6a16-889f-8581-fc16e8165ac0). 

The following table lists credentials for [!include[interface](../includes/product-short.md)]:

| Credentials | Name |
|--|--|
| PI Data server | [!include[interface](../includes/dir-short.md)]_X_PI |
| PI Asset Framework | [!include[interface](../includes/dir-short.md)]_X_AF |
| Batch interface data source | [!include[interface](../includes/dir-short.md)]_X_Source_Y |

**Notes:** 

* `X` is a placeholder for an interface instance **Service ID**.
* `Y` is a placeholder for a data source instance number.

## To update credentials

If you need to update the credentials that the interface uses for authentication, edit the configuration settings for the instance using PI Event Frames Interface Manager.

1. From **Interface Selection**, select the applicable [!include[interface](../includes/product-short.md)] instance.

1. From **Server Information**, update the credentials used to authenticate with PI Data server or PI Asset Framework.

1. From **Source**, update the credentials used to authenticate with a data source. 
   
1. Click **Save Settings**.

**Result:** The credentials are updated within the instance configuration. Restart the interface to update the credentials within Windows Credentials Manager.
