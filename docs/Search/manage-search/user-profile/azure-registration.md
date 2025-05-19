---
title: Azure Registration
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

Azure Active Directory (Azure AD) registration allows Unbxd to integrate with SSO (Single Sign-On) for secure user authentication. This process enables the customer to authenticate users through Azure AD without requiring separate credentials for Unbxd. The configuration involves registering the Unbxd application in the Azure portal and finalizing settings in the Unbxd console.

> 📘 Note
>
> Azure Registration will be done by the Customer support team. Netcore Unbxd **do not** have access to their Azure Active Directory

## Registration Steps

1. **Steps to Register Application in Azure Portal**\
   Navigate to Enterprise applications in Azure AD. Go to **Azure Active Directory** > **Enterprise Applications**. Click on Click **New application** > **Create your own application**. Give a name for the application **Unbxd SSO** and select **Integrate any other application you don’t find in the gallery (Non-gallery)** option. Click **Create**.

<br />

2. **Configure Single Sign-On (SSO)**\
   Once the application is created, navigate to **Single sign-on** >  **SAML**. In Basic SAML Configuration, enter the following details from the Unbxd console:

<Table>
  <thead>
    <tr>
      <th>
        **Field**
      </th>

      <th>
        **Description**
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        **Identifier (Entity ID)**
      </td>

      <td>
        A unique identity that identifies the service provider (Unbxd) in SAML transactions. Example: `Unbxd_SSO`
        It could be anything but should match with field `Identifier (Entity ID)`
      </td>
    </tr>

    <tr>
      <td>
        **Reply URL (Assertion Consumer Service URL)**
      </td>

      <td>
        The endpoint where Azure AD sends the authentication response after a successful sign-in.
        Example: `https://console.unbxd.io/login/callback/`
      </td>
    </tr>

    <tr>
      <td>
        **(Optional) Sign-on URL**
      </td>

      <td>
        The URL where users can initiate the login process.
        Example: `https://your-unbxd-app.com/login`
      </td>
    </tr>

    <tr>
      <td>
        **Attributes & Claims**
      </td>

      <td>
        claim **emailaddress** should be preset and point to user's email ID
      </td>
    </tr>
  </tbody>
</Table>

3. **Assign Users and Groups**\
   Navigate to Users and Groups in the Azure AD portal. Click **Add user/group**. Select the users or groups that should have access to Unbxd via SSO. Click **Assign**.
4. **Finalize Configuration in Unbxd**\
   Log in to your Unbxd account. Navigate to SSO Settings under profile. Enter the below required Information

Save the configuration and test the login.