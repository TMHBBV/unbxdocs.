---
title: Browser Integration
deprecated: false
hidden: false
metadata:
  robots: index
---
# JavaScript Based Integration

With Browser Integration, you can insert the unique tracker, as a custom Javascript file, anywhere within the HTML pages in your website for all the various events. As a first step we need to include UnbxdAnalytics.js script to the head of all the HTML pages, where we want the track functionality to work. You can add it using the below code to you HTML:

```
<script type="text/javascript">
  var UnbxdSiteName = "{{site-key}}"; // Replace the value with the Site Key.
  var UnbxdApiKey = "{{api-key}}"; // Replace the value with API key
  (function() {
    var ubx = document.createElement('script');
    ubx.type = 'text/javascript';
    ubx.async = true;
    ubx.src = '//libraries.unbxdapi.com/ua-js/v1.0.0/uaLibrary.js';
    (document.getElementsByTagName('head')[0] || document.getElementsByTagName('body')[0]).appendChild(ubx);
  })();
</script>
```

NOTE: UnbxdSiteName should be initialized with the correct site key for the environment of your account in Unbxd.

Visitor\
This event is used to track shoppers and make their user profiles using browser cookies. To enable this event we just need to add Unbxd’s analytics JS library (as done above) inside the head section of all pages of the site.

NOTE: The visitor event will be fired from the SDK itself. If you have integrated the Unbxd analytics JS code, this event is tracked and pushed automatically, with no further action required.

The Visitor event is the first event that gets created when a shopper visits your site.  There are two types of shoppers we track:

First-time shoppers\
Repeat shoppers
Experience Impression
A recommendation(experience) impression event is fired when a recommendation widget results loads on Home, Product, Category, Cart or Brand page. For each of these actions, unique Ids of the products visible on the recommendation widget on any above page should be sent as payload.

```
<script type="text/javascript">
	var payload = {
             requestId: '{{unbxd-request-id}}',
		pids_list: '{{list-of-products-uniqueId}}',
		experience_pagetype: '{{recs-pagetype}}',
		experience_widget: '{{recs-widget}}'
	}
	var action = 'experience_impression'
	if(Unbxd && typeof Unbxd.track === 'function') {
		Unbxd.track(action, payload)
	} else {
		console.error('unbxdAnalytics.js is not loaded!')
	}
</script>
```

Payload details:

| **Attribute Name**   | **Datatype** | **What Value to be Passed**                                                                                                                 |
| -------------------- | ------------ | ------------------------------------------------------------------------------------------------------------------------------------------- |
| requestId            | string       | To be extracted from Unbxd search API response headers, from `unx-request-id`                                                               |
| pids\_list           | string       | List of unique IDs of products loaded with the current request. If zero products are returned, pass an empty list (array).                  |
| experience\_pagetype | string       | Pagetype for widget. Possible values: `Home`, `Product`, `Category`, `Cart`, `Brand` based on the type of page on which the widget is used. |
| experience\_widget   | string       | Widget type. Possible values: `WIDGET1`, `WIDGET2`, or `WIDGET3`.                                                                           |

Product Click\
The click event should be tracked whenever a user clicks on any product to go to the product details page. It should have the information about the source of the product listing which will a recommendation widget in this case.

```
<script type="text/javascript">
	var payload = {
		pid: '{{unique-id}}',
		prank: '{{number-of-product}}',
		experience_pagetype: '{{recs-pagetype}}',
		experience_widget: '{{recs-widget}}',
		requestId: '{{unbxd-request-id}}'
	}
	if(Unbxd && typeof Unbxd.track === 'function') {
		Unbxd.track('click', payload)
	} else {
		console.error('unbxdAnalytics.js is not loaded!')
	}
</script>
```

Payload details:

| **Attribute Name**   | **Datatype** | **What Value to be Passed**                                                                                                                 |
| -------------------- | ------------ | ------------------------------------------------------------------------------------------------------------------------------------------- |
| requestId            | string       | To be extracted from Unbxd search API response headers, from `unx-request-id`                                                               |
| pid                  | string       | Unique ID for the product                                                                                                                   |
| variantId            | string       | Variant ID of the selected product variant, if `relevantDocumentType="variant"`, from search API response, or null if not applicable.       |
| prank                | string       | Rank (number) of the product in the search response                                                                                         |
| experience\_pagetype | string       | Pagetype for widget. Possible values: `Home`, `Product`, `Category`, `Cart`, `Brand` based on the type of page on which the widget is used. |
| experience\_widget   | string       | Widget type. Possible values: `WIDGET1`, `WIDGET2`, or `WIDGET3`.                                                                           |

Product View\
Product Page View indicates the total number of visits that has been made to the product details page (PDP) by the visitor irrespective of the source (search result page, category page, search engine, email, marketing campaigns, etc).The product view can be tracked whenever a user lands on the PDP page.

\<script type="text/javascript">
&#x20; var payload = \{
&#x20;   pid: '\{\{uniqueId-of-the-product}}',
&#x20;   variantId: '\{\{variantId-of-selected-variant}}'
&#x20; }
&#x20; if(Unbxd && typeof Unbxd.track === 'function') \{
&#x20;   Unbxd.track('product\_view', payload)
&#x20; } else \{
&#x20;   console.error('unbxdAnalytics.js is not loaded!')
&#x20; }
\</script>

Payload details:

## Add to Cart

Whenever a user adds any product to cart or shopping bag, the add to cart will get fired. This helps us further improve the products appearing in the Recommendation widget.

```
Add to Cart
Whenever a user adds any product to cart or shopping bag, the add to cart will get fired. This helps us further improve the products appearing in the Recommendation widget.
```

Payload:

| **Datatype** | **What Value to be Passed**                                                                                                                      |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| string       | Unique ID for the product, to be taken from API response, if `relevantDocumentType="parent"`, in search API response, or null if not applicable. |
| string       | The variant ID of the selected product variant, if `relevantDocumentType="variant"`, in search API response, or null if not applicable.          |
| string       | Quantity being added to the cart by the user.                                                                                                    |
| string       | The unit price of the product (or variant, if a variant is selected).                                                                            |

Cart Removal\
Whenever a user removes any product from cart or discards the whole cart. The cart removal event should be tracked individually for all products being removed.

```
<script type="text/javascript">
  var payload = {
    pid: '{{uniqueId-of-the-product}}',
    variantId: '{{variantId-of-selected-variant}}',
    qty: '{{quantity-selected}}',
    price: '{{unit-price-for-product}}',
  }
  if(Unbxd && typeof Unbxd.track === 'function') {
    Unbxd.track('cartRemoval', payload)
  } else {
    console.error('unbxdAnalytics.js is not loaded!')
  }
</script>
```

Payload details:

| **Attribute Name** | **Datatype** | **What Value to be Passed**                                                                                                                      |
| ------------------ | ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| pid                | string       | Unique ID for the product, to be taken from API response, if `relevantDocumentType="parent"`, in search API response, or null if not applicable. |
| variantId          | string       | Variant ID of the selected product variant, if `relevantDocumentType="variant"`, in search API response, or null if not applicable.              |
| qty                | string       | Quantity being removed by the user, as a string.                                                                                                 |
| price              | string       | Unit price of the product (or variant, if a variant is selected), as a string.                                                                   |

Order\
When a user completes the transaction and lands on the order confirmation/success page, the order event should be tracked for each individual product. There are 2 ways to trigger the order event and either of them can be used:

1. Individually for all even

```
<script type="text/javascript">
  var payload = {
    pid: '{{uniqueId-of-the-product}}',
    variantId: '{{variantId-of-selected-variant}}',
    qty: '{{quantity-selected}}',
    price: '{{unit-price-for-product}}'
  }
  if(Unbxd && typeof Unbxd.track === 'function') {
    Unbxd.track('order', payload)
  } else {
    console.error('unbxdAnalytics.js is not loaded!')
  }
</script>
```

Payload Details:

| **Attribute Name** | **Datatype** | **What Value to be Passed**                                                                                                                      |
| ------------------ | ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| price              | string       | Unit price of the product (or variant, if variant is selected), as a string.                                                                     |
| pid                | string       | Unique ID for the product, to be taken from API response, if `relevantDocumentType="parent"`, in search API response, or null if not applicable. |
| variantId          | string       | Variant ID of the selected product variant, if `relevantDocumentType="variant"`, in search API response, or null if not applicable.              |
| qty                | string       | Quantity being removed by the user, as a string.                                                                                                 |

<br />

OR

Individually for all events

```
<script type="text/javascript">
  var payload = [
   {
    pid: '{{uniqueId-of-the-product}}',
    variantId: '{{variantId-of-selected-variant}}',
    qty: '{{quantity-selected}}',
    price: '{{unit-price-for-product}}'
    },
    {
    pid: '{{uniqueId-of-the-product}}',
    variantId: '{{variantId-of-selected-variant}}',
    qty: '{{quantity-selected}}',
    price: '{{unit-price-for-product}}'
    }
  ]
  if(Unbxd && typeof Unbxd.track === 'function') {
    Unbxd.trackMultiple('order', payload)
  } else {
    console.error('unbxdAnalytics.js is not loaded!')
  }
</script>
```