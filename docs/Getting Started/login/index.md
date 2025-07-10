---
title: Login
deprecated: false
hidden: false
metadata:
  robots: index
---

Netcore Unbxd supports a **hybrid login system**, offering flexibility and security for both internal employees and external collaborators. Depending on your organization's setup, users can authenticate using **SSO (Single Sign-On)** or traditional **Credential-based login (email \+ password)**, with optional **Two-Factor Authentication (2FA)**.

## Types of Login

| Login Type                 | Description                                                       |
| :------------------------- | :---------------------------------------------------------------- |
| **SSO Login**              | Users authenticate through your organization’s identity provider. |
| **Credential-based Login** | Users log in using an email and password combination.             |

Admins can assign the appropriate login method during the **user invitation** process.

### **When SSO is Used**

- The **default method** is when SSO is enabled at the **account level**.
- Used by **internal employees** for seamless, centralized access.
- Users are automatically redirected to the organization's SSO provider.
- **Credential login is blocked** unless explicitly overridden for the user.

### **When Credential-based Login is Used**

- This is for **external collaborators**, contractors, or non-SSO users.
- Admins can **override the SSO default** during user invitation to allow email/password access.
- Used when the user is **not part of the SSO directory** or needs limited access.

### **When 2FA is Triggered**

- 2FA is only applicable for **credential-based login**.
- When **enabled at the account level**, all users logging in via email/password will:
  1. Enter their credentials
  2. Be prompted to complete a 2FA verification step (e.g., OTP)


Once SSO is enabled for any account, two-factor authentication gets disabled automatically for that particular account.