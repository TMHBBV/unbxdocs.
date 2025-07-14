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

# Events

Events are any action a visitor takes on your eCommerce store.

Once deployed, the JS code tracks shopper events, using information stored within a cookie titled ‘unbxd.userId’. This file tracks, stores, and relays useful session-based information to Unbxd.

This section helps you understand more about the session-based events we track, like:

* **Visitor**: Identifies new and returning shoppers.
* **Experience Impression**: Is used to track the products viewed in recommendation widgets for Similar products, Recommended for You, etc.
* Product Click: Is when a shopper clicks on a product in the PLP.
* Product View: Is the number of times a shopper has visited a specific Product Details Page (PDP).
* Add to Cart: Is the number of times shoppers have added products to a cart. This event can be fired from both PDP and PLP.
* Cart Removal: Is the number of times a shopper has removed a product from the cart.
* Orders: Is the number of orders that have been successfully completed.

# API Integration

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

* X-Forwarded-For

**user-agent**

## **Visitor**

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

## Search Hit

The Search event is generated every time a shopper uses the search bar to search for a product on your site.

Here’s how a Search API will look like.

```
http://tracker.unbxdapi.com/v2/1p.jpg?data={"query":"{{search-query}}","url":"{{url-of-the-website}}","referrer":"","requestId":"{{unx-request-id}}","visit_type":"{{first_or_repeat}}","visitId":"{{visit-id}}"}&UnbxdKey={{unbxd-sitekey}}&action=search&uid={{uid}}5&t=1662365253141|0.6835012308821242
```

> 📘 NOTE
>
> Action for this event will be “search”, as in the API above and does not need to be changed.

| **Attribute Name** | **Datatype** | **What Value to be Passed**                                                                                   |                      |
| :----------------- | :----------- | :------------------------------------------------------------------------------------------------------------ | :------------------- |
| `action`           | string       | Indicates the type of event. For search events, the value will be `'search'`.                                 |                      |
| `query`            | string       | The search query entered by the user.                                                                         |                      |
| `pid`              | string       | Unique ID for the product (from API response) if `relevantDocumentType = "parent"`. Otherwise, can be `null`. |                      |
| `url`              | string       | Website URL where the search is performed.                                                                    |                      |
| `requestId`        | string       | Extract from Unbxd Search API response headers, from the `unx-request-id` value.                              |                      |
| `visit_type`       | string       | Indicates if the visit is a `"first_time"` or `"repeat"` visit.                                               |                      |
| `UnbxdKey`         | string       | Value of the `UnbxdSiteKey`.                                                                                  |                      |
| `uid`              | string       | Extract from the `unbxd.userId` cookie. This is the unique identifier for the shopper.                        |                      |
| `t`                | –            | Timestamp in the format: \`new Date().getTime() + '                                                           | ' + Math.random();\` |
| `referrer`         | string       | (Optional) The link or page URL from which the search page was accessed.                                      |                      |

## Search Impression

A Search Impression (also known as Product Impressions) event is generated after a shopper gets a list of products on the search results page. This event is also generated every time a shopper refines the results by facets, filters, scroll-down or pagination. The productId of the products listed in the PLP will be sent as a payload.

Here’s how a Search Impression API will look like.

```
https://tracker.unbxdapi.com/v2/1p.jpg?data={"query":"{{search-query}}","pids_list":"{{list-of-products-uniqueId}}","url":"{{url-of-the-website}}","referrer":"","requestId":"{{unx-request-id}}","visit_type":"{{first_or_repeat}}",,,"visitId":"{{visit-id}}"}&UnbxdKey={{unbxd-sitekey}}&action=search_impression&uid={{uid}}&t=1662366285967|0.7498946341398707  
```

<br />

| **Attribute Name** | **Datatype** | **What Value to be Passed**                                                                                        |                      |
| :----------------- | :----------- | :----------------------------------------------------------------------------------------------------------------- | :------------------- |
| `action`           | string       | Indicates the type of event. For search impression events, the value will be `'search_impression'`.                |                      |
| `query`            | string       | The search query entered by the user.                                                                              |                      |
| `url`              | string       | Website URL where the search is performed.                                                                         |                      |
| `pids_list`        | string       | List of unique product IDs returned in the current response. If no products are returned, pass an **empty array**. |                      |
| `requestId`        | string       | Extract from the Unbxd Search API response headers, under the key `unx-request-id`.                                |                      |
| `visit_type`       | string       | Indicates if the visit is a `"first_time"` or `"repeat"` visit.                                                    |                      |
| `UnbxdKey`         | string       | The Unbxd Site Key (`UnbxdSitekey` value).                                                                         |                      |
| `uid`              | string       | Extract from the cookie `unbxd.userId`. This is the unique identifier for the shopper.                             |                      |
| `t`                | –            | Timestamp formatted as: \`new Date().getTime() + '                                                                 | ' + Math.random();\` |
| `referrer`         | string       | (Optional) URL of the page from which the search page was opened.                                                  |                      |

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

## Orders

The Orders event is pushed for every product that is purchased on your site.

Here’s how an Order API will look like.

```
https://tracker.unbxdapi.com/v2/1p.jpg?data={"pid":"{{uniqueId-of-the-product}}","qty":"{{quantity-selected}}","price":"{{unit-price-for-product}}","url":"{{url-of-the-website}}","referrer":"","visit_type":"{{first_or_repeat}}","requestId":"{{unx-request-id}}","visitId":"{{visit-id}}"}&UnbxdKey={{unbxd-sitekey}}&action=order&uid={{uid}}1658904085468-92302&t=1662367087116|0.07798836811209986
```

Payload details:

| **Attribute Name** | **Datatype** | **What Value to be Passed**                                                                    |
| ------------------ | ------------ | ---------------------------------------------------------------------------------------------- |
| `action`           | string       | Indicates the type of event. For order events, the value will be `'order'`.                    |
| `query`            | string       | The search query entered by the user.                                                          |
| `pid`              | string       | Unique ID for the product from API response (if `relevantDocumentType = "parent"`), or `null`. |
| `price`            | string       | Unit price of the product (variant price if a variant is selected).                            |
| `url`              | string       | URL of the **order success page** where the order event API is fired.                          |
| `requestId`        | string       | Extracted from Unbxd Search API response headers, under the key `unx-request-id`.              |
| `visit_type`       | string       | Indicates if the visit is a `"first_time"` or `"repeat"` visit.                                |
| `UnbxdKey`         | string       | The Unbxd Site Key (`UnbxdSitekey` value).                                                     |
| `uid`              | string       | Extract from the cookie `unbxd.userId`. This is the unique identifier for the shopper.         |
| `referrer`         | string       | *(Optional)* The URL of the page from which the order success page was opened.                 |

## Facets

A Facet event tracks the guided navigation on the Product Listing Page. The event query will list the specific filters the shopper has selected to narrow down the results on the search results page.

Here is how the API call will look like when facets are clicked on search page:

```
http://tracker.unbxdapi.com/v2/1p.jpg?data={"query":"{{search-query}}","facets":{“facet-name”:[value],},"url":"{{url-of-the-website}}","referrer":"","requestId":"{{unx-request-id}}","visit_type":"{{first_or_repeat}}","visitId":"{{visit-id}}"}&UnbxdKey={{unbxd-sitekey}}&action=search&uid={{uid}}5&t=1662365253141|0.6835012308821242
```

> 📘 NOTE
>
> Action for this event will be “search”, as in the API above and does not need to be changed.

| **Attribute Name** | **Datatype** | **What Value to be Passed**                                                                                                                                          |                      |
| :----------------- | :----------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------- |
| `action`           | string       | Indicates the type of event. For this case, the value will be `'search'`.                                                                                            |                      |
| `query`            | string       | The search query entered by the user.                                                                                                                                |                      |
| `facets`           | string       | JSON key-value pair of selected facets. \<br>Example: \`"facets": \{ "flavour\_uFilter": \["Orange", "Cola"], "goal\_categoryPath\_uFilter": \["Daily Wellness"] }\` |                      |
| `pid`              | string       | Unique product ID from the API response (if `relevantDocumentType = "parent"`), or `null`.                                                                           |                      |
| `url`              | string       | Website URL where the search is performed.                                                                                                                           |                      |
| `requestId`        | string       | Extracted from the Unbxd Search API response headers (`unx-request-id`).                                                                                             |                      |
| `visit_type`       | string       | Indicates if the visit is a `"first_time"` or `"repeat"` visit.                                                                                                      |                      |
| `UnbxdKey`         | string       | The Unbxd Site Key (`UnbxdSitekey` value).                                                                                                                           |                      |
| `uid`              | string       | Extracted from the cookie `unbxd.userId`. This is the unique shopper identifier.                                                                                     |                      |
| `t`                | string       | Timestamp string: \`new Date().getTime() + '                                                                                                                         | ' + Math.random();\` |
| `referrer`         | string       | *(Optional)* The URL from which the current page was opened.                                                                                                         |                      |

## Autosuggest

If the autocomplete feature on store is powered by Unbxd, then events originating from Unbxd Autosuggest Widget should pass additional metadata. This enables us to improve autocomplete suggestions over time. It is also used to generate reports on how well different types of suggestions are doing.

### Events from Autosuggest

In this section we will give examples of events which may originate from the user’s interaction with Autosuggest widget and hence should send suggestion related metadata with payload. This will cover Javascript based approach for integrating the events.

### Search

Whenever a user selects any suggestion from Autosuggest widget and hits the form submit, this event should be tracked. It should also send additional information about the suggestion using autosuggestParams field in the payload.

For instance in case of infield suggestion like below:

<Image align="center" border={true} caption="Infield Suggestion" src="https://files.readme.io/41e482537ffe730f525ad67862d0ae2019ad34d339311cbe5a3fd5ce68156933-image.png" width="80% " />

On submitting the form (irrespective of mouse or keyboard) any of the options (including popular products) from the autocomplete box should trigger a search event which should provide autosuggest related metadata. The image beacon looks like this when selecting the “Batman” option from the suggestion list.

<Image align="center" className="border" border={true} width="80% " src="https://files.readme.io/69da188f230631babaee6f19f9dba3a27df10fe1730813a0daff4cf4ca141769-image.png" />

<br />

The Unbxd.track API call will look like this:

1. In case, it is an IN\_FIELD suggestion which is selected and submitted:

```
https://tracker.unbxdapi.com/v2/1p.jpg?data={"query":"{{suggested-query}}","autosuggest_data":{"autosuggest_type":"IN_FIELD","autosuggest_suggestion":"{{suggested-query}}","field_value":null,"field_name":null,"src_field":null,"pid":null,"internal_query":"{{original-query}}"},"url":"{{url-of-the-website}}","referrer":"","visit_type":"{{first_or_repeat}}","visitId":"{{visit-id}}"}&UnbxdKey={{unbxd-sitekey}}&action=search&uid={{uid}}&t=1666830840426|0.12139712486982823
```

<br />

| **Attribute Name**       | **Datatype** | **What Value to be Passed**                                                                                                            |
| ------------------------ | ------------ | -------------------------------------------------------------------------------------------------------------------------------------- |
| `autosuggest_type`       | string       | The autosuggest type. For IN\_FIELD suggestions, this will typically be `'IN_FIELD'` (same as the `doctype` in Unbxd Autosuggest API). |
| `autosuggest_suggestion` | string       | The suggested query from the in-field suggestion.                                                                                      |
| `field_name`             | string       | Name of the field used for the IN\_FIELD suggestion.                                                                                   |
| `field_value`            | string       | The value of the selected field (i.e., the actual suggestion).                                                                         |
| `internal_query`         | string       | The typed query in the search box that triggered the autosuggest results.                                                              |
| `query`                  | string       | The final suggested query (same as `autosuggest_suggestion`).                                                                          |
| `url`                    | string       | Website URL where the search was performed.                                                                                            |
| `requestId`              | string       | Extracted from the Unbxd Search API response headers (`unx-request-id`).                                                               |
| `visit_type`             | string       | Indicates if the visit is `"first_time"` or `"repeat"`.                                                                                |
| `UnbxdKey`               | string       | The Unbxd Site Key (`UnbxdSitekey` value).                                                                                             |
| `uid`                    | string       | Extracted from the cookie `unbxd.userId`. This is the unique shopper ID.                                                               |
| `referrer`               | string       | *(Optional)* The URL of the page from which the search was initiated.                                                                  |

2. In case, it is POPULAR\_PRODUCTS suggestion which is selected and submitted:

```
https://tracker.unbxdapi.com/v2/1p.jpg?data={"query":"{{suggested-query}}","autosuggest_data":{"autosuggest_type":"POPULAR_PRODUCTS","autosuggest_suggestion":"{{suggested-query}}","field_value":null,"field_name":null,"src_field":null,"pid":"{{uniqueId-of-the-product}}","unbxdprank":"{{rank-of-product}}","internal_query":"{{original-query}}"},"url":"{{url-of-the-website}}","referrer":"","visit_type":"{{first_or_repeat}}","visitId":"{{visit-id}}"}&UnbxdKey={{unbxd-sitekey}}&action=search&uid={{uid}}&t=1666851030913|0.2127782620243308
```

| **Attribute Name** | **Datatype** | **What Value to be Passed**                                                                                                    |
| ------------------ | ------------ | ------------------------------------------------------------------------------------------------------------------------------ |
| `autosuggest_type` | string       | Should be `'POPULAR_PRODUCTS'` depending on the suggestion type. Usually same as the `doctype` from the Unbxd Autosuggest API. |
| `pid`              | string       | Unique ID of the selected product (from the API response).                                                                     |
| `unbxdprank`       | string       | Rank of the product in the autosuggest list (specific to POPULAR\_PRODUCTS).                                                   |
| `internal_query`   | string       | The typed query in the search box that triggered the autosuggest results.                                                      |
| `query`            | string       | The suggested query in keyword or infield. Can be `null` for POPULAR\_PRODUCTS selections.                                     |
| `url`              | string       | Website URL where the search is performed.                                                                                     |
| `requestId`        | string       | Extracted from Unbxd Search API response headers (`unx-request-id`).                                                           |
| `visit_type`       | string       | Indicates whether the user visit is `"first_time"` or `"repeat"`.                                                              |
| `UnbxdKey`         | string       | The Unbxd Site Key (`UnbxdSitekey` value).                                                                                     |
| `uid`              | string       | Unique shopper ID extracted from the `unbxd.userId` cookie.                                                                    |
| `referrer`         | string       | *(Optional)* The URL of the page from which the autosuggest was triggered.                                                     |

3. In case, it is an KEYWORD\_SUGGESTIONS which is selected and submitted:

```
https://tracker.unbxdapi.com/v2/1p.jpg?data={"query":"{{suggested-query}}","autosuggest_data":{"autosuggest_type":"KEYWORD_SUGGESTION","autosuggest_suggestion":"{{suggested-query}}","field_value":null,"field_name":null,"src_field":null,"pid":null,"unbxdprank":"{{rank-of-product}}","internal_query":"{{original-query}}"},"url":"{{url-of-the-website}}","referrer":"","visit_type":"{{first_or_repeat}}","visitId":"{{visit-id}}"}&UnbxdKey={{unbxd-sitekey}}&action=search&uid={{uid}}&t=1666830840426|0.12139712486982823
```

Payload details:

| **Attribute Name**       | **Datatype** | **What Value to be Passed**                                                                   |
| ------------------------ | ------------ | --------------------------------------------------------------------------------------------- |
| `autosuggest_type`       | string       | Set to `'KEYWORD_SUGGESTION'`. Same as the `doctype` field in the Unbxd Autosuggest API.      |
| `autosuggest_suggestion` | string       | The suggested query shown in autosuggest.                                                     |
| `field_name`             | string       | The field used for the keyword suggestion.                                                    |
| `field_value`            | string       | The value of the field used for the suggestion.                                               |
| `internal_query`         | string       | The typed query entered by the user in the search box that triggered the autosuggest results. |
| `query`                  | string       | The final suggested query from the keyword suggestion.                                        |
| `url`                    | string       | Website URL where the search is performed.                                                    |
| `requestId`              | string       | Extracted from the Unbxd Search API response headers (`unx-request-id`).                      |
| `visit_type`             | string       | Indicates whether the visit is `"first_time"` or `"repeat"`.                                  |
| `UnbxdKey`               | string       | The Unbxd Site Key (`UnbxdSitekey` value).                                                    |
| `uid`                    | string       | Unique shopper ID, extracted from the `unbxd.userId` cookie.                                  |
| `referrer`               | string       | *(Optional)* URL of the page from where the search or autosuggest was initiated.              |

## Click

This event should be tracked (along with search) whenever any popular product option is clicked on the autocomplete box.

The Unbxd.track API call will look like this and will be based on the selection type:

```
https://tracker.unbxdapi.com/v2/1p.jpg?data={"query":"{{suggested-query}}","autosuggest_data":{"autosuggest_type":"{{autosuggest-type}}","autosuggest_suggestion":"{{suggested-query}}","field_value":null,"field_name":{{suggestion-field-name}},"src_field":{{src-field}},"pid":"{{uniqueId-of-the-product}}","unbxdprank":"{{rank-of-product}}","internal_query":"{{original-query}}"},"url":"{{url-of-the-website}}","referrer":"","visit_type":"{{first_or_repeat}}","visitId":"{{visit-id}}"}&UnbxdKey={{unbxd-sitekey}}&action=click&uid={{uid}}&t=1666851030913|0.2127782620243308
```

Payload details:

| **Attribute Name**       | **Datatype** | **What Value to be Passed**                                                                             |
| ------------------------ | ------------ | ------------------------------------------------------------------------------------------------------- |
| `autosuggest_type`       | string       | Should be `'POPULAR_PRODUCT'`, depending on the selected suggestion type.                               |
| `autosuggest_suggestion` | string       | Suggested query in keyword or infield. Can be `null` if a POPULAR\_PRODUCT is selected.                 |
| `field_name`             | string       | For `IN_FIELD` suggestions, this is the name of the field used. Should be `null` for POPULAR\_PRODUCT.  |
| `field_value`            | string       | For `IN_FIELD` suggestions, this is the value of the suggestion. Should be `null` for POPULAR\_PRODUCT. |
| `pid`                    | string       | Unique ID of the selected product, from the autosuggest API response.                                   |
| `unbxdprank`             | string       | Rank of the selected product (1-based index), applicable to POPULAR\_PRODUCT.                           |
| `internal_query`         | string       | The typed query entered by the user into the search box that triggered autosuggest.                     |
| `query`                  | string       | Suggested query from autosuggest. Can be `null` for POPULAR\_PRODUCT.                                   |
| `url`                    | string       | Website URL where the search was performed.                                                             |
| `requestId`              | string       | Extracted from the Unbxd Search API response headers (`unx-request-id`).                                |
| `visit_type`             | string       | Indicates whether the visit is `"first_time"` or `"repeat"`.                                            |
| `UnbxdKey`               | string       | The Unbxd Site Key (`UnbxdSitekey` value).                                                              |
| `uid`                    | string       | Unique shopper identifier, extracted from the `unbxd.userId` cookie.                                    |
| `referrer`               | string       | *(Optional)* The URL of the page from which the autosuggest interaction was initiated.                  |

## Add to Cart

This event should be tracked whenever any product is added to cart directly from the autocomplete box.

The Unbxd.track call will look like below:

```
https://tracker.unbxdapi.com/v2/1p.jpg?data={"pid":"{{uniqueId-of-the-product}}","qty":”{{no-of-units}}","variantId":"{{variantId-of-the-variant}}",”price”:”{{price-of-the-product}}”,"autosuggest_data":{"autosuggest_type":"POPULAR_PRODUCTS","autosuggest_suggestion":"{{suggested-query}}""field_name":{{fiel-name}},"field_value":{{field-value}},"src_field":null,"pid":"{{uniqueId-of-the-product}}","unbxdprank":null,"internal_query":null}",url":"{{url-of-the-website}}","referrer":"","visit_type":"{{first-or-repeat}}","requestId":"{{request-id}}"&UnbxdKey=”{{unbxd-sitekey}}&action=cart&uid={{uid}}&t={{time-spent}}
```

Payload details:

| **Attribute Name**       | **Datatype** | **What Value to be Passed**                                                                                      |
| ------------------------ | ------------ | ---------------------------------------------------------------------------------------------------------------- |
| `autosuggest_type`       | string       | Can be one of: `IN_FIELD`, `KEYWORD_SUGGESTION`, or `POPULAR_PRODUCT`, depending on the selected suggestion.     |
| `autosuggest_suggestion` | string       | Suggested query in keyword or infield. Can be `null` if `POPULAR_PRODUCT` is selected.                           |
| `field_name`             | string       | For `IN_FIELD` suggestions: name of the field. For others: `null`.                                               |
| `field_value`            | string       | For `IN_FIELD` suggestions: value of the field. For others: `null`.                                              |
| `pid`                    | string       | For `POPULAR_PRODUCT`: pass `uniqueId` of the selected product. For `IN_FIELD` and `KEYWORD_SUGGESTION`: `null`. |
| `unbxdprank`             | string       | For `POPULAR_PRODUCT`: rank of the product (1-based). For others: `null`.                                        |
| `internal_query`         | string       | The typed query entered in the search box that led to the autosuggest results.                                   |
| `query`                  | string       | The final suggested query submitted from autosuggest. Can be `null` if `POPULAR_PRODUCT` is selected.            |
| `url`                    | string       | Website URL where the search is performed.                                                                       |
| `requestId`              | string       | Extracted from the Unbxd Search API response headers (`unx-request-id`).                                         |
| `visit_type`             | string       | Indicates whether the user visit is `"first_time"` or `"repeat"`.                                                |
| `UnbxdKey`               | string       | The Unbxd Site Key (`UnbxdSitekey`).                                                                             |
| `uid`                    | string       | Unique shopper ID, extracted from the cookie `unbxd.userId`.                                                     |
| `referrer`               | string       | *(Optional)* The URL from which the autosuggest interaction or page was in                                       |