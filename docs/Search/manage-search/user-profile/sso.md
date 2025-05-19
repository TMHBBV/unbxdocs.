---
title: SSO
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

Single Sign-On (SSO) is an authentication process that allows users to access multiple applications with a single set of credentials. It enhances security, reduces user effort, and simplifies credential management.

## Prerequisites

> 📘 Note
>
> The user must be registered for the Azure App. This registration is done by the Netcore Unbxd support team.

Before proceeding, make sure the following points are covered.

1. An Azure Active Directory tenant with admin access.
2. A Netcore Unbxd account should be present with admin privileges.
3. A registered custom domain in Azure AD.

### Benefits of SSO

* Centralized Security: Authenticate users through your IdP for enhanced security.
* Simplified Access: Eliminate the need for multiple credentials.
* Enterprise-Ready: Compatible with providers like Microsoft Azure and supports SAML 2.0.

## Configure Single Sign on for Netcore Unbxd

Sign in to your Netcore Unbxd account Panel. Navigate to **Profile**  > **SSO**.

> 👍 Important
>
> Once the user account is registered in **Azure AD** for Unbxd application, then you would be able to enable button on the SSO screen under profile section. Refer to [Azure Registration]() For SSO

Once account is enabled in Azure AD, enter the below details (Azure help desk will share the details) and save the configuration.

* Ensure the **App federation Metadata URL** from Azure AD is mapped to **Metadata URL** in the Netcore Unbxd panel.
* Ensure the **Login URL** from Azure AD is mapped to**Login URL** in the Netcore Unbxd panel.