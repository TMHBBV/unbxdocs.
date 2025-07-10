---
title: Analytics Compliance
deprecated: false
hidden: false
metadata:
  robots: index
---
# Is your integration GDPR compliant?

When implementing Unbxd's Analytics Tracking service on your ecommerce website, ensuring compliance with the General Data Protection Regulation (GDPR) is crucial. Here’s how to maintain GDPR compliance while using our service:

## User Consent Handling

Default Behavior: By default, the trackAnalytics flag is set to true, which enables tracking for all users. However, it is essential to handle user consent appropriately.

## Tracking Consent

1. User Accepts Tracking: If a user consents to tracking their session data (either by accepting all cookies or specific categories related to session tracking), you should call the Unbxd.enableAnalytics() function to enable tracking for that session.
2. User Denies Tracking: If a user denies consent for tracking, either by rejecting all cookies or specific categories, call the Unbxd.disableAnalytics() function to stop tracking for that session.

<br />

## Persistent User Preferences

Once a user has made their choice regarding consent preferences, it's vital to store this preference locally, such as in a cookie or local storage. This practice ensures that you can respect the user’s decision across multiple sessions. On subsequent visits, check the stored preference and call Unbxd.enableAnalytics() or Unbxd.disableAnalytics() accordingly.

### How to implement, disable, or enable tracking?

1. Initialization

Ensure you have included the Unbxd Analytics JavaScript file in your HTML:

```
 <script src="https://libraries.unbxdapi.com/sdk-clients/PROD_SITEKEY/ua/ua.js">
 </script>
```

Replace PROD\_SITEKEY with your actual production site key.

2. <br />