---
title: User Profile
excerpt: >-
  This is the section where you manage your account details including your
  profile, your team members, and your created sites. 
deprecated: false
hidden: false
metadata:
  robots: index
---
# User Management Overview

Manage user accounts, permissions, and roles within your system or application. You can edit the details by clicking the **Avatar** at the right-most corner of the console. Navigate to **My profile**.

## Profile

You can view and update your personal information, preferences, and account settings.

| **Profile Section** | **Description**                                                        |
| ------------------- | ---------------------------------------------------------------------- |
| **Name**            | Your full name to personalize your profile.                            |
| **Email**           | Your email address for notifications and account updates.              |
| **Organization**    | Your company or organization for tailored services.                    |
| **Website**         | Link your website to connect your account with your business presence. |
| **TimeZone**        | Your timezone to adjust your settings and notifications accordingly.   |

## Team Management

You can organize and manage team members, assign roles, and control access to features. Navigate to User Management > **Team Management**. Click on "+" symbol to add new team members. Input the email address of the new member and assign their appropriate role. The roles and their accesses is explained below:

<Table>
  <thead>
    <tr>
      <th>
        **Role**
      </th>

      <th>
        **Access**
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        **Owner**
      </td>

      <td>
        * Add sites
        * Add team members
        * has access to merchandising, view reports
        * Can add synonyms, create banners

        **This role cannot be assigned to multiple people in the team. The email registered during onboarding is made the owner of the account**.
      </td>
    </tr>

    <tr>
      <td>
        **Admin**
      </td>

      <td>
        Can do everything as an owner can, except add sites.Can control team management if the user is admin of all the sites across the account.
      </td>
    </tr>

    <tr>
      <td>
        **Merchandiser**
      </td>

      <td>
        Can do everything an owner can, except add sites and team management.
      </td>
    </tr>

    <tr>
      <td>
        **Analyst (Search Product)**
      </td>

      <td>
        Can only read query rules, view reports, and see the Configure site tab. Cannot add/edit a campaign or query rule.
      </td>
    </tr>

    <tr>
      <td>
        **Analyst (Browse Product)**
      </td>

      <td>
        Can only read page rules, view reports, and see the Configure site tab. Cannot add/edit a campaign or page rule. Can add/edit segments.
      </td>
    </tr>

    <tr>
      <td>
        **Developer**
      </td>

      <td>
        Can access reports and configure the site section.\
        Cannot add a site, do team management, or access page/query rules.
      </td>
    </tr>

    <tr>
      <td>
        **No-access**
      </td>

      <td>
        Cannot access anything for the site.
      </td>
    </tr>
  </tbody>
</Table>

## My Sites

The list of multiple sites added for your profile are displayed here with the following details:

| **Field**                    | **Description**                                                 |
| ---------------------------- | --------------------------------------------------------------- |
| **Number of sites allotted** | The maximum number of allowed sites you can add.                |
| **Number of sites added**    | The number of sites you have added out of the allotted number.  |
| **Remaining**                | The remaining number of sites that you can still add.           |
| **Min Campaign Duration**    | The defined duration for which the campaign will remain active. |

## SSO

Single Sign-On (SSO) is an authentication process that allows users to access multiple applications with a single set of credentials. It enhances security, reduces user effort, and simplifies credential management.\
If your organization uses SSO to sign in to applications, you can register with Azure AD to use the same credentials.
Follow the link below to learn how to register on Azure Active Directory. Registration must be completed by users individually:  Azure Registration For SSO
Prerequisites:
An Azure AD tenant with admin access.
A Unbxd account with admin privileges.
A registered custom domain in Azure AD.
Enabling SSO Login for Unbxd
Unbxd supports SSO using SAML 2.0 and functions as an SSO service provider. SAML (Security Assertion Markup Language) is a standard for exchanging authentication and authorization data between an identity provider and a service provider.

This is how your account will look if SSO is not enabled.