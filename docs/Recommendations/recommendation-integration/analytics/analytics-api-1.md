---
title: Analytics API
deprecated: false
hidden: false
metadata:
  robots: index
---
# Introduction​

Whether you’re a large enterprise or an SME (small-to-medium enterprise) online store owner, your resources are finite. As your business grows, your shoppers are looking for a retail experience that is intuitive and personalized.

Tracking visitor analytics and behaviour anonymously is critical to provide accurate and visitor-specific search and category page results.

To help us analyse and understand your shoppers better, Unbxd captures information for every visitor anonymously by creating the following three sets of cookies:

userId: An identifier for the shopper. This cookie never expires.\
visitId – An identifier for the session/visit. This cookie expires when the shopper is idle for more than 30 minutes.
visit – This stores whether the visitor is a ‘first\_time’ or ‘repeat’ shopper. This cookie expires when the shopper is idle for more than 30 minutes.
NOTE: Session cookies have an inactivity timer. Sessions expire when they are idle for more than 30 minutes.

The information within these cookies are used to create a non-identifiable persona that allows us to analyze your shopper’s past click-through behaviors, shopping history, and product preferences, in real time. We use this information to provide site-level aggregate reporting.

Unique tracking codes within site interactions help us measure the performance user interactions anonymously.

Anonymous shopper profiles help fetch personalized search results. It also helps in generating detailed reports.

In other words, information is aggregated and analysed for two purposes:

Providing relevant and personalised search & category pages results\
Generating reports
As a merchandiser or product manager you can make informed decisions and make your shopper’s experience a delightful one.

Events\
Events are any action a visitor takes on your eCommerce store.

Once deployed, the JS code tracks shopper events, using information stored within a cookie titled ‘unbxd.userId’. This file tracks, stores, and relays useful session-based information to Unbxd.

This section helps you understand more about the session-based events we track, like:

Visitor: Identifies new and returning shoppers.\
Experience Impression: Is used to track the products viewed in recommendation widgets for Similar products, Recommended for You, etc.
Product Click: Is when a shopper clicks on a product in the PLP.
Product View: Is the number of times a shopper has visited a specific Product Details Page (PDP).
Add to Cart: Is the number of times shoppers have added products to a cart. This event can be fired from both PDP and PLP.
Cart Removal: Is the number of times a shopper has removed a product from the cart.
Orders: Is the number of orders that have been successfully completed.
API Integration
In this method, you integrate the API references for every event that you want Unbxd to track.

NOTE: In case you are using a web browser, it is recommended that you use the Browser-based integration.

The calls have to be in the form of an http GET request to the url:

```
tracker.unbxdapi.com/v2/1p.jpg
```

Some of the common attributes used in the APIs are described below:

**referrer**: The url of the previous page, will be empty if the user opened that particular url directly.\
**uid**: The unique identifying number for shoppers. Usually we set the “uid” for a particular user in a particular browser. The “uid” is stored within the “uid” cookie, and we store this ID every time we need user-specific event information.
Every request needs to be passed with the following HTTP headers:

X-Forwarded-For

* **user-agent**
* **Visitor**

This event is used to track shoppers and make their user profiles using browser cookies. To enable this event we just need to add Unbxd’s analytics JS library (as done above) inside the head section of all pages of the site.

> 📘 NOTE
>
> The visitor event will be fired from the SDK itself. If you have integrated the Unbxd analytics JS code, this event is tracked and pushed automatically, with no further action required.

The Visitor event is the first event that gets created when a shopper visits your site.  There are two types of shoppers we track:

* **First-time shoppers**
* **Repeat shoppers**

Here’s how a Visitor API will look like.

```
https://tracker.unbxdapi.com/v2/1p.jpg?data={"url":"{{url-of-the-website}}","referrer":"{{reference-link}}","visit_type":"{{first-or-repeat}}","visitId":"{{visitId}}"}&UnbxdKey={{unbxd_sitekey}}&action=”visitor”&uid=”uid-1642414737751-2003”&t=”1662364656435|0.29442892143527755”
```

Payload Details:

| **Attribute Name** | **Datatype** | **What value to be passed**                                                                               |                      |
| ------------------ | ------------ | --------------------------------------------------------------------------------------------------------- | -------------------- |
| `action`           | String       | Indicates the type of event. In this case, the value will be ‘visitor’.                                   |                      |
| `url`              | String       | Website URL where search is performed.                                                                    |                      |
| `visit_type`       | String       | Can be either “first\_time” or “repeat”.                                                                  |                      |
| `UnbxdKey`         | String       | UnbxdSitekey value.                                                                                       |                      |
| `uid`              | String       | Need to be extracted from the cookie, `unbxd.userId`. This is the unique identifying number for shoppers. |                      |
| `t`                | String       | Timestamp parameter should be calculated as follows: \`t = new Date().getTime() + ‘                       | ’ + Math.random();\` |
| `referrer`         | String       | Link from where the page is opened (optional).                                                            |                      |

Experience impression\
A recommendation(experience) impression event is fired when a recommendation widget results loads on Home, Product, Category, Cart or Brand page. For each of these actions, unique Ids of the products visible on the recommendation widget on any above page should be sent as payload.

Here’s how a Visitor API will look like.

```
https://tracker.unbxdapi.com/v2/1p.jpg?data={"experience_pagetype":"{{recs-pagetype}}","experience_widget":"{{recs-widget}}","pids_list":["LIST OF UNIQUE ID OF PRODUCTS"],"url":"{{url-of-the-website}}","referrer":"","requestId":"{{unx-request-id}}","visit_type":"{{first_or_repeat}}","visitId":"{{visit-id}}"}&UnbxdKey={{unbxd-sitekey}}&action=experience_impression&uid={uid}&t=1662365577295|0.5578634723619054
```

<br />

| **Attribute Name**    | **Datatype** | **What value to be passed**                                                                                                               |
| --------------------- | ------------ | ----------------------------------------------------------------------------------------------------------------------------------------- |
| `action`              | String       | Indicates the type of event. In this case, the value will be ‘experience\_impression’.                                                    |
| `experience_pagetype` | String       | Pagetype for the widget should be either Home, Product, Category, Cart, or Brand based on the type of page on which the widget is used.   |
| `experience_widget`   | String       | Widget type, either WIDGET1, WIDGET2, or WIDGET3.                                                                                         |
| `pids_list`           | String       | Unique IDs for the products, to be taken from the Recs API response, if `relevantDocumentType="parent"`. In Recs API response, or `null`. |
| `url`                 | String       | Website URL where the search is performed.                                                                                                |
| `qty`                 | String       | Quantity being removed by the user, as a string.                                                                                          |
| `requestId`           | String       | To be extracted from the Unbxd search API response headers, from `unx-request-id`.                                                        |

## Product Click

The Product Click event is generated every time a shopper clicks on a product in a Product Listing Page (PLP).

This helps us understand your shoppers’ search preferences. This information is analyzed to list and promote ‘Popular Products’ and display personalized ‘Recommended For You’ lists.

Here’s how a Product Click API will look like.

```
https://tracker.unbxdapi.com/v2/1p.jpg?data={"pid":"{{uniqueId-of-the-product}}","pr":"","experience_pagetype":"{{recs-pagetype}}","experience_widget":"{{recs-widget}}","requestId":"{{unx-request-id}}","url":"{{url-of-the-website}}","referrer":"","visit_type":"{{first_or_repeat}}","ver":"4.0.28","_uf":1187461382,"visitId":"{{visit-id}}"}&UnbxdKey={{unbxd-sitekey}}&action=click&uid={uid}}&t=1662365583875|0.7442797542869459
```

Payload Details:

| **Attribute Name**    | **Datatype** | **What value to be passed**                                                                                                             |
| --------------------- | ------------ | --------------------------------------------------------------------------------------------------------------------------------------- |
| `action`              | String       | Indicates the type of event. In this case, the value will be ‘click’.                                                                   |
| `experience_pagetype` | String       | Pagetype for the widget should be either Home, Product, Category, Cart, or Brand based on the type of page on which the widget is used. |
| `experience_widget`   | String       | Widget type, either WIDGET1, WIDGET2, or WIDGET3.                                                                                       |
| `url`                 | String       | Website URL where the product is clicked.                                                                                               |
| `pid`                 | String       | Unique ID of the product viewed.                                                                                                        |
| `requestId`           | String       | To be extracted from the Unbxd search API response headers, from `unx-request-id`.                                                      |
| `visit_type`          | String       | Can be either “first\_time” or “repeat”.                                                                                                |

## Product View

Product View indicates the total number of visits that has been made to the product details page (PDP) by the visitor irrespective of the source (search result page, category page, search engine, email, marketing campaigns, etc). The product view can be tracked whenever a user lands on the PDP page.

```
https://tracker.unbxdapi.com/v2/1p.jpg?data={"pid":"{{uniqueid-of-the-product}}","referrer":"","url":"{{url-of-the-website}}",”variantId”:”{{variantId-of-the-variant}}”,"visit_type":"{{first-or-repeat}}","requestId":”{{request-id}},”UnbxdKey”=”{{unbxd-sitekey}}&action=product_view,”uid”:”{{uid}}”&t={{time-spent}} 
```

Payload Details:

| **Attribute Name** | **Datatype** | **What value to be passed**                                                                               |                                                                                                |
| ------------------ | ------------ | --------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| `action`           | String       | Indicates the type of event. In this case, the value will be ‘product\_view’.                             |                                                                                                |
| `url`              | String       | URL of the product display page (PDP), on which the product is viewed.                                    |                                                                                                |
| `pid`              | String       | Unique ID of the product viewed.                                                                          |                                                                                                |
| `requestId`        | String       | To be extracted from the Unbxd search API response headers, from `unx-request-id`.                        |                                                                                                |
| `visit_type`       | String       | Can be either “first\_time” or “repeat”.                                                                  |                                                                                                |
| `UnbxdKey`         | String       | UnbxdSitekey value.                                                                                       |                                                                                                |
| `uid`              | String       | Need to be extracted from the cookie, `unbxd.userId`. This is the unique identifying number for shoppers. |                                                                                                |
| `t`                | String       | This timestamp parameter should be calculated as follows: \`t = new Date().getTime() + ‘                  | ’ + Math.random();\`. This timestamp parameter will be autogenerated while making an API call. |
| `referrer`         | String       | Link from where the page is opened (optional).                                                            |                                                                                                |

## Add to Cart

Whenever a user adds any product to cart or shopping bag, the add to cart will get fired.This help us further improve product ranks for a Recommendation implementation.

```
https://tracker.unbxdapi.com/v2/1p.jpg?data={"pid":"{{uniqueid-of-the-product}}","qty":”{{no-of-units}}","variantId":"{{variantId-of-the-variant}}","url":"{{url-of-the-website}}","referrer":"","visit_type":"{{first-or-repeat}}","requestId":"{{request-id}}"&UnbxdKey=”{{unbxd-sitekey}}&action=cart&uid={{uid}}&t={{current_time | random number between 0 to 1}} 
```

Payload details:

| **Attribute Name** | **Datatype** | **What value to be passed**                                                                                                                                                               |
| ------------------ | ------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `action`           | String       | Indicates the type of event. In this case, the value will be ‘cart’.                                                                                                                      |
| `qty`              | String       | The number of units added to the cart. This should be the string value of the quantity added. For example, if 2 quantities of a product are added, its value would be “2” (instead of 2). |
| `url`              | String       | URL of the page where the product is added to the cart.                                                                                                                                   |
| `pid`              | String       | Unique ID of the product viewed.                                                                                                                                                          |
| `requestId`        | String       | To be extracted from the Unbxd search API response headers, from `unx-request-id`.                                                                                                        |
| `visit_type`       | String       | Can be either “first\_time” or “repeat”.                                                                                                                                                  |
| `UnbxdKey`         | String       | UnbxdSitekey value.                                                                                                                                                                       |
| `uid`              | String       | Need to be extracted from the cookie, \`unbxd.                                                                                                                                            |

## Cart Removal

The Remove From Cart event tracks every instance a product is removed from cart as well. Information helps us better understand the visitor’s preferences. When a product with variants is removed from the cart, here’s how the API will look like.

```
https://tracker.unbxdapi.com/v2/1p.jpg?data={"pid":"{{uniqueId-of-the-product}}","variantId":"{{variantId-of-the-variant}}","qty":"{{no_of_units}}","url":"{{url-of-the-website}}","requestId":"{{unx-request-id}}","referrer":"","visit_type":"{{first_or_repeat}}","ver":"4.0.28","_uf":1187461382,"visitId":"{{visit-id}}"}&UnbxdKey={{unbxd-sitekey}}&action=cartRemoval&uid={uid}}&t=1662365583875|0.7442797542869459
```

Payload Details:

| **Attribute Name** | **Datatype** | **What value to be passed**                                                                               |
| ------------------ | ------------ | --------------------------------------------------------------------------------------------------------- |
| `action`           | String       | Indicates the type of event. In this case, the value will be ‘cartRemoval’.                               |
| `url`              | String       | URL of the page where the product is removed from the cart.                                               |
| `pid`              | String       | Unique ID of the product viewed.                                                                          |
| `variantId`        | String       | VariantId of the variant-product. It is necessary only if variants are present. (optional)                |
| `qty`              | String       | Quantity being removed by the user, as a string.                                                          |
| `requestId`        | String       | To be extracted from the Unbxd search API response headers, from `unx-request-id`.                        |
| `uid`              | String       | Need to be extracted from the cookie, `unbxd.userId`. This is the unique identifying number for shoppers. |
| `visit_type`       | String       | Can be either “first\_time” or “repeat”.                                                                  |
| `UnbxdKey`         | String       | UnbxdSitekey value.                                                                                       |
| `variantId`        | String       | VariantId of the variant-product. It is necessary only if variants are present. (optional)                |
| `referrer`         | String       | Link from where the page is opened (optional).                                                            |

## Orders

The Orders event is pushed for every product that is purchased on your site. When a product with variants is purchased from the website.

Here’s how an Order API will look like.

```
https://tracker.unbxdapi.com/v2/1p.jpg?data={"pid":"{{uniqueId-of-the-product}}","qty":"{{no_of_units}}","price":"{{unit-price-for-product}}","url":"{{url-of-the-website}}","referrer":"","visit_type":"{{first_or_repeat}}","requestId":"{{unx-request-id}}","visitId":"{{unx-request-id}}"}&UnbxdKey={{unbxd-sitekey}}&action=order&uid={uid}}&t=1662367087116|0.07798836811209986
```

Payload Details:

| **Attribute Name** | **Datatype** | **What value to be passed**                                                                               |
| ------------------ | ------------ | --------------------------------------------------------------------------------------------------------- |
| `action`           | String       | Indicates the type of event. In this case, the value will be ‘order’.                                     |
| `url`              | String       | URL of the order success page where the API for the order event is fired.                                 |
| `variantId`        | String       | VariantId of the variant-product. It is necessary only if variants are present. (optional)                |
| `qty`              | String       | Quantity being removed by the user, as a string.                                                          |
| `requestId`        | String       | To be extracted from the Unbxd search API response headers, from `unx-request-id`.                        |
| `uid`              | String       | Need to be extracted from the cookie, `unbxd.userId`. This is the unique identifying number for shoppers. |
| `visit_type`       | String       | Can be either “first\_time” or “repeat”.                                                                  |
| `UnbxdKey`         | String       | UnbxdSitekey value.                                                                                       |