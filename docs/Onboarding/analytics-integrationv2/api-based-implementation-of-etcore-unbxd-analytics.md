---
title: API-based Implementation of etcore Unbxd Analytics
deprecated: false
hidden: false
metadata:
  robots: index
---
> 📘 Note
>
> Integration method recommended by Netcore Unbxd onboarding experts.

One of the ways you can implement Netcore Unbxd Analytics is with the help of APIs. Our API provides effortless, anonymous tracking of visitor behavior, enabling personalized search and category page results based on individual preferences. Additionally, the API powers comprehensive, site-level reporting.

<br />

## Things to Do Before API (GET) Integration (Prerequisites)

## 1. Add the common and event-specific attributes

To ensure a successful API implementation, it’s essential to cross-verify or create the necessary attributes. You can get a detailed understanding of the API call here. These attributes fall into two categories:

* Common Attributes: Applied universally across all events and critical for consistent tracking (e.g., user ID, timestamp).
* Event-Specific Attributes: Unique to individual events, capturing details specific to an interaction (e.g., product ID for click events).

> 📘 Note
>
> Both common and event-specific attributes are mandatory. Attribute names and types must EXACTLY match those provided in the documentation.

## 2. Add Autosuggest attributes

If your autosuggest widget is powered by Netcore Unbxd, then you’ll have to fire a few additional events. These will help improve autosuggest accuracy and provide necessary reports.

## 3. Pass the Request with the Following HTTP Headers

| Parameter         | Description                                                                                                                                                                   | Significance                                                                 |
| :---------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------- |
| `user-agent`      | Browser identification information is passed to the web server with every HTTPS request.                                                                                      | If not passed, device-based merchandising campaigns will not work.           |
| `X-Forwarded-For` | Signifies the IP address of the end-user. This is required primarily if the integration is a backend process since Unbxd doesn’t get the IP of the end-user from the browser. | If not passed, segmentation, A/B testing, and personalization will not work. |