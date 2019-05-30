---
title: Restrict access to Azure AD administration portal
date: 2019-05-30T22:46:37.867Z
description: >-
  [I-AAD0001] Restrict access to Azure AD administration portal to prevent
  Non-Admin Users from access.
---
```
Finding ID: I-AAD0001Risk: CAT IIISource: Azure Active DirectoryDescription: Access to Azure AD Administration Portal is not restricted.
```

## Background

The default option of “No” pertaining to the **Restrict access to Azure AD administration portal** setting “lets a non-administrator use this Azure AD administration portal experience to access Azure AD resources that the user has permission to read, or manage resources they own.”

## Protect

Selecting the Option “Yes” pertaining to the Restrict access to Azure AD administration portal setting “restricts all non-administrators from accessing any Azure AD data in the administration portal.”

* This setting does not restrict such access using PowerShell or another client such as Visual Studio.

1. Login to Azure Tenant with an account that has Global Administrator rights within the Azure tenant.
2. Within the Azure Tenant, navigate to Azure Active Directory blade and select Users, then select User Settings.

![Azure Active Directory Tenant – User Properties – Restrict access to Azure AD administration portal.](/img/azure-inno-ad-01_001.png "Azure Active Directory Tenant – User Properties – Restrict access to Azure AD administration portal.")

1. In the User Settings options, locate Administration portal section, under this heading Select the Yes for the Restrict access to Azure AD administration portal setting.

![Azure Active Directory Tenant – User Properties – Restrict access to Azure AD administration portal.](/img/azure-inno-ad-01_002.png "Azure Active Directory Tenant – User Properties – Restrict access to Azure AD administration portal.")

## Exposure

Administrative Portal access can be access by any “standard” or “non-admin” account. Described below are example access methods Pre and Post Protection. 

> Non-Administrative User's have this access granted by default.

Example: A standard Enterprise user, logging in to Azure Management Portal.

* Azure Portal URL : `portal.azure.com`

![Azure Active Directory Tenant – User Properties – Restrict access to Azure AD administration portal.](/img/azure-inno-ad-03.png "Azure Active Directory Tenant – User Properties – Restrict access to Azure AD administration portal.")

* Once Portal Access Restriction is enabled, Non-Admin accessing Azure Management Portal is presented “Access Denied”

![Azure Active Directory Tenant – User Properties – Restrict access to Azure AD administration portal.](/img/azure-inno-ad-04.png "Azure Active Directory Tenant – User Properties – Restrict access to Azure AD administration portal.")

> Portal Access Control Restriction does not prevent access to Azure AD information via other methods. 

The below examples step through what a Non-Admin user can still query to AAD.

```
Method: PowershellModule: AzureADConnect-AzureAD $CredentialsGet-AzureADUser | select DisplayName
```

```
Method: PowershellModule: Azaz loginGet-AzADUser | select DisplayName
```

```
Method: PowershellModule: MsolConnect-MsolService $CredentialsGet-MsolUser | select DisplayName
```
