---
title: Google Tag Manager Integration
excerpt: >-
  llows you to manage and deploy marketing tags on your website without having
  to modify the code
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

Tracking visitor analytics and behavior are essential in order to provide accurate and visitor-specific search and category page results. UNBXD analyzes visitor events, such as product clicks, products added to cart, orders, etc. These events are tracked using browser cookies. With this information, a profile is built for every visitor, based on his/her affinity to different categories, brands, or prices.

This information is then aggregated and analyzed for two purposes:

1. Generating reports
2. Providing relevant and personalized search & category pages results

When visitors browse through your store, the integrated trackers log everything visitors do – the products they visit, orders, even the various store properties they interact with. We take that information, analyze it, and assemble a detailed profile of the visitor. We know their browsing patterns, preferences and can even determine susceptibility to merchandising campaigns. The trackers are unique tracking codes that must be configured onto the store properties that yield an interaction. We call this interaction as an “event”, for example, click on the “Add to Cart” button.

The visitor profiles help fetch relevant and personalized products as search results. It also helps in generating detailed reports.

> 📘 Note
>
> For Unbxd E-commerce Search to function correctly on your site, Unbxd Analytics must be configured.

## Introduction to GTM

Google Tag Manager is a free tool that allows you to manage and deploy marketing tags (snippets of code or tracking pixels) on your website (or mobile app) without having to modify the code.

**Working of GTM**:

Information from one data source (your website) is shared with another data source (Analytics) through Google Tag Manager. GTM becomes very handy when you have lots of tags to manage because all the code is stored in one place.

**Basic components of Google Tag Manager:**

| **Component** | **Details**                                                                                            | **Example**                                                                                    |
| ------------- | ------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------- |
| **Tags**      | Tracking codes and code fragments that instruct GTM what action to take on a page.                     | Sending searched query to Unbxd analytics.                                                     |
| **Triggers**  | Conditions that specify when a tag should fire.                                                        | A trigger that fires a tag when a user views URLs containing the path `/search/`.              |
| **Variables** | Values used in triggers and tags to filter when a specific tag should fire. Can be built-in or custom. | A ‘click’ class variable has a value assigned to buttons on the website (e.g., a word string). |
| **DataLayer** | A JSON object containing name-value pairs of data points to be passed from a website to GTM.           | DataLayer passes user data such as search query to Unbxd tags via GTM.                         |

### Prerequisites

The below criteria needs to be met before Netcore Unbxd starts tracking through GTM:

* Unbxd analytics scripts need to be loaded across all the pages. We require a tag which will need to be loaded on all the pages. Below is the required code block for Unbxd analytics script. This should be loaded before other Unbxd tracking scripts and is mandatory to be added on all pages.

```Text Java
// Container ID is present in GTM-XXXX format in GTM Dashboard
// HTML ID can be found in the url. Eg:
// containers/422XXXX/workspaces/20 , 20 is the HTML ID

<script type = "text/javascript" >
   /* * * CONFIGURATION * * */
   // Replace the value with the Unbxd Site Key and API Key.

   var UnbxdSiteName = "{{UNBXD_SITE_NAME}}";
   var UnbxdApiKey = "{{UNBXD_API_KEY}}";

   /* * * DON'T EDIT BELOW THIS LINE * * */
   (function() {
   var ubx = document.createElement('script');
   ubx.type = 'text/javascript';
   ubx.async = true; ubx.src='//d21gpk1vhmjuf5.cloudfront.net/unbxdAnalytics.js';
   ubx.addEventListener('load', function() {
   window.google_tag_manager[{{Container ID}}].onHtmlSuccess({{HTML ID}}); });
   (document.getElementsByTagName('head')[0] || document.getElementsByTagName('body')[0]).appendChild(ubx);
   })();
</script>
```

> ❗️ Important
>
> The above JS snippet needs to be added in a tag and also enable Built-In Variables, i.e., Container ID and HTML ID without fail.
>
> * TagName: UnbxdAnalyticsScript
> * TagType: Custom HTML Tag
> * Trigger: AllPagesPageView

## Search Query Tracker

A Search hit event is tracked to understand the query and intent of your visitors. Each search query is tracked to enable per-query analytics of the visitor. A typical search hit event involves:

**SearchQueryTrigger** Through GTM to integrate this event we need to follow below approach:

1. Create Trigger in GTM to catch the search Query on form hit.\
   Trigger Configuration:

| **Component**        | **Details**             |
| -------------------- | ----------------------- |
| **Trigger Name**     | UnbxdSearchQueryTrigger |
| **Trigger Type**     | Custom Event            |
| **Event Name**       | SearchQuery             |
| **Trigger Fires On** | All custom events       |

<Image align="center" className="border" border={true} width="80% " src="https://files.readme.io/4e53e4ed9f185d5bbf7c28c0f1a30ad49ae385a64c298c9ac7c5a3ccf754ca77-image.png" />

2. Create Variable in GTM, to fetch the query from the dataLayer.\
   Variable Configuration:

| **Component**                | **Details**             |
| ---------------------------- | ----------------------- |
| **Variable Name**            | UnbxdSearchQueryPayload |
| **Variable Type**            | Data Layer Variable     |
| **Data Layer Variable Name** | SearchQueryPayload      |

HTML Content:

<Image align="center" width="80% " src="https://files.readme.io/3b6111a47330804ccbd5b040acb1aaadc6500860eecfba496a05201605da0f4d-image.png" />

<br />

3. Create a Javascript tag with the below details.

| **Component** | **Details**         |
| ------------- | ------------------- |
| **Tag Name**  | UnbxdSearchQueryTag |
| **Tag Type**  | Custom HTML         |

```
// Pass payload to Unbxd.track function
// to call the tracker API

<script type="text/javascript">
   var u_payload = {{UnbxdSearchQueryPayload}};
   if (Unbxd && typeof Unbxd.track === 'function'
       && u_payload.hasOwnProperty("query")) {
       Unbxd.track("search", u_payload);
   } else {
       console.error('unbxdAnalytics.js is not loaded or payload incorrect!')
   }
</script>
```

4. Pushing the event to the dataLayer through a search query.

| **Attribute** | **Datatype** | **Value to be passed**                                                        |
| ------------- | ------------ | ----------------------------------------------------------------------------- |
| **requestId** | string       | To be extracted from Unbxd search API response headers, from `unx-request-id` |
| **query**     | string       | The search query used by the user                                             |