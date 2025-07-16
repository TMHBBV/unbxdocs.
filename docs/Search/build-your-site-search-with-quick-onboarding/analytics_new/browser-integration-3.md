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

### Visitor

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

## Product View

Product Page View indicates the total number of visits that has been made to the product details page (PDP) by the visitor irrespective of the source (search result page, category page, search engine, email, marketing campaigns, etc).The product view can be tracked whenever a user lands on the PDP page.

<script type="text/javascript">
  var payload = \{
  pid: '\{\{uniqueId-of-the-product}}',
  variantId: '\{\{variantId-of-selected-variant}}'
  }
  if(Unbxd && typeof Unbxd.track === 'function') \{
  Unbxd.track('product\_view', payload)
  } else \{
  console.error('unbxdAnalytics.js is not loaded!')
  }
</script>

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

### Cart Removal

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

### Order

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

## Facets

A Facet event tracks the guided navigation on the Product Listing Page. The event query will list the specific filters the shopper has selected to narrow down the results on the search results page.

> 📘 NOTE
>
> In case of SDK integration, we do not have to add this event explicitly and is handled by the SDK itself and requestId is also handled by SDK integration. Please ensure that unbxdAnalytics flag is set as “true” to allow this event to fire automatically.

```
<script type="text/javascript">
  var payload = {
    query: '{{search-query}}',
    facets: {'facet_name':['facet_value','facet_value'],'facet_name':['facet_value']},
    requestId: '{{unbxd-request-id}}'
  }
  if(Unbxd && typeof Unbxd.track === 'function') {
    Unbxd.track('facets', payload)
  } else {
    console.error('unbxdAnalytics.js is not loaded!')
  }
</script>
```

Payload details:

### Attributes for Event Tracking

| Attribute Name | Datatype | What value to be passed                                                            |
| -------------- | -------- | ---------------------------------------------------------------------------------- |
| `requestId`    | string   | To be extracted from Unbxd search API response headers, from `unx-request-id`      |
| `facets`       | object   | Should contain key-value pairs of selected facet names and list of selected values |
| `query`        | string   | Search query for the search listing page                                           |

### Autosuggest

If the autocomplete feature on store is powered by Unbxd, then events originating from Unbxd Autosuggest Widget should pass additional metadata. This enables us to improve autocomplete suggestions over time. It is also used to generate reports on how well different types of suggestions are doing.

**Events from Autosuggest**

In this section we will give examples of events which may originate from the user’s interaction with Autosuggest widget and hence should send suggestion related metadata with payload. This will cover Javascript based approach for integrating the events.

**Search**

Whenever a user selects any suggestion from Autosuggest widget and hits the form submit, this event should be tracked. It should also send additional information about the suggestion using autosuggestParams field in the payload.

On submitting the form (irrespective of mouse or keyboard) any of the options (including popular products) from the autocomplete box should trigger a search event which should provide autosuggest related metadata. The image beacon looks like this when selecting the “Batman” option from the suggestion list.

<br />

The Unbxd.track call will look like this based on the type of suggestion selected:

1. In case, it is an IN\_FIELD suggestion which is selected and submitted:

```
<script type='text/javascript'>
var payload = {
  query: '',
  autosuggestParams: {
    autosuggest_type: 'IN_FIELD',
    autosuggest_suggestion: '{{suggested-query}}',
    field_name: '{{name-of-field}}',
    field_value: '{{infield-value}}',
    src_field: '{{src-field-name}}'',
    internal_query: '{{original-query}}'
  }
}
if(Unbxd && typeof Unbxd.track === 'function') {
  Unbxd.track('search', payload)
} else {
  console.error('unbxdAnalytics.js is not loaded!')
}
</script>
```

<br />

### Attributes for Autosuggest Event Tracking

| Attribute Name           | Datatype | What value to be passed                                                               |
| ------------------------ | -------- | ------------------------------------------------------------------------------------- |
| `event_type`             | string   | `'Search'` needs to be passed as event in `Unbxd.track`                               |
| `autosuggest_type`       | string   | `IN_FIELD`, usually the same as the value of `doctype` field in Unbxd autosuggest API |
| `autosuggest_suggestion` | string   | Suggested query in `IN_FIELD` that is selected                                        |
| `field_name`             | string   | In case of `IN_FIELD` suggestions, the name of the field which is used for suggestion |
| `field_value`            | string   | In case of `IN_FIELD` suggestions, the value of the field, which is the suggestion    |
| `src_field`              | string   | Source field, can be passed empty                                                     |
| `internal_query`         | string   | The typed query in search box, which led to the suggestions in autosuggest            |

<br />

2. In case, it is POPULAR\_PRODUCTS suggestion which is selected and submitted:

```
<script type='text/javascript'>
var payload = {
  query: '',
  autosuggestParams: {
   autosuggest_type: 'POPULAR_PRODUCTS',
   pid: '{{uniqueId-of-the-product}}',
   unbxdprank: '{{rank-of-product}}',
   internal_query: '{{original-query}}'
  }
}
if(Unbxd && typeof Unbxd.track === 'function') {
  Unbxd.track('search', payload)
} else {
  console.error('unbxdAnalytics.js is not loaded!')
}
</script>
```

<br />

### Attributes for Popular Products Autosuggest Event Tracking

| Attribute Name     | Datatype | What value to be passed                                                                       |
| ------------------ | -------- | --------------------------------------------------------------------------------------------- |
| `event_type`       | string   | `'Search'` needs to be passed as event in `Unbxd.track`                                       |
| `autosuggest_type` | string   | `POPULAR_PRODUCTS`, usually the same as the value of `doctype` field in Unbxd autosuggest API |
| `pid`              | string   | `uniqueId` of the selected popular product                                                    |
| `unbxdprank`       | string   | In case of `POPULAR_PRODUCTS` suggestions, the rank of the product                            |
| `internal_query`   | string   | The typed query in search box, which led to the suggestions in autosuggest                    |

3. In case, it is KEYWORD\_SUGGESTION suggestion which is selected and submitted:

```
<script type='text/javascript'>
var payload = {
  query: '',
  autosuggestParams: {
    autosuggest_type: 'KEYWORD_SUGGESTION',
    autosuggest_suggestion: '{{suggested-query}}',
    field_name: '{{name-of-field}}',
    field_value: '{{infield-value}}',
    src_field: '{{src-field-name}}'',
    internal_query: '{{original-query}}'
  }
}
if(Unbxd && typeof Unbxd.track === 'function') {
  Unbxd.track('search', payload)
} else {
  console.error('unbxdAnalytics.js is not loaded!')
}
</script>
```

Payload details:

### Attributes for Keyword Suggestion Autosuggest Event Tracking

| Attribute Name           | Datatype | What value to be passed                                                                             |
| ------------------------ | -------- | --------------------------------------------------------------------------------------------------- |
| `event_type`             | string   | `'Search'` needs to be passed as event in `Unbxd.track`                                             |
| `autosuggest_type`       | string   | `KEYWORD_SUGGESTION`, usually the same as the value of the `doctype` field in Unbxd autosuggest API |
| `autosuggest_suggestion` | string   | Suggested query in keyword                                                                          |
| `field_name`             | string   | Name of the field used for suggestion in case of `KEYWORD` suggestions                              |
| `field_value`            | string   | Value of the field, which is the suggestion                                                         |
| `src_field`              | string   | Source field, can be passed empty                                                                   |
| `internal_query`         | string   | The typed query in the search box which led to the suggestions in autosuggest                       |

<br />

**Click**

NOTE: Autosuggest click event only needs to be fired in the case of popular product suggestions when it directly redirects to PDP.

This event should be tracked (along with search) whenever any popular product option is clicked on the autocomplete box. Similar to payload in search from autosuggest, we can have different payload conditions when an In field or a popular product is selected respectively.

```
<script type='text/javascript'>
var payload = {
  pid: "{{uniqueId-of-the-products}}",
  prank: "{{rank-of-product}}"
}
if(Unbxd && typeof Unbxd.track === 'function') {
  Unbxd.track('click', payload)
} else {
  console.error('unbxdAnalytics.js is not loaded!')
}
</script>
```

Add to Cart

### Attributes for Add to Cart Tracking

| Attribute Name | Datatype | What value to be passed                                                                      |
| -------------- | -------- | -------------------------------------------------------------------------------------------- |
| `pid`          | string   | UniqueId of the selected product                                                             |
| `variantId`    | string   | VariantId of the selected product variant (if `relevantDocumentType = "variant"`), or `null` |
| `qty`          | string   | Quantity being added to the cart by the user                                                 |

This event should be tracked whenever any product is added to cart directly from the autocomplete box.

```
<script type='text/javascript'>
var payload = {
  pid: '{{uniqueId-of-the-products}}',
  variantId: '{{variantId-of-the-products}}', //only if the variants are true
  qty: '{{number-of-quantities-added-to-the-cart}}',
}
if(Unbxd && typeof Unbxd.track === 'function') {
  Unbxd.track('addToCart', payload)
} else {
  console.error('unbxdAnalytics.js is not loaded!')
}
</script>
```

### Attributes for Popular Product Selection Tracking

| Attribute Name | Datatype | What value to be passed                                                                    |
| -------------- | -------- | ------------------------------------------------------------------------------------------ |
| `pid`          | string   | In case of a popular product getting selected, pass the `uniqueId` of the selected product |
| `unbxdprank`   | string   | For `POPULAR_PRODUCTS` suggestions, the rank (1-based index) of the product                |

# HTML Based Integration

With Browser Integration, you can insert the unique tracker, as a custom Javascript file, anywhere within the HTML pages in your website for all the various events. As a first step we need to include UnbxdAnalytics.js script to the head of all the HTML pages, where we want the track functionality to work. You can add it using the below code to you HTML:

Sample Request:

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

<div unbxdAttr="product" unbxdparam_sku="{{uniqueId-of-product}}" />

Also, add the script below before Unbxd analytics library is loaded.

```
<script type="text/javascript">
UnbxdAnalyticsConf=window.UnbxdAnalyticsConf ||{};
UnbxdAnalyticsConf["experience_pagetype"]="{{recs-pagetype}}";
UnbxdAnalyticsConf["experience_widget"]="{{recs-widget}}";
</script>
```

Parameter details:

| **Attribute Name**    | **Datatype** | **What value to be passed**                                                                                        |
| --------------------- | ------------ | ------------------------------------------------------------------------------------------------------------------ |
| `unbxdattr`           | Constant     | Specifies the type of event being captured. For product clicks, the value is “product” always.                     |
| `unbxdparam_sku`      | Variable     | Specifies the uniqueId of the product as defined in the feed. You can get this from the UNBXD search API response. |
| `experience_pagetype` | Variable     | Pagetype for the widget should be either Home, Product, Category,\_                                                |

### Visitor

This event is used to track shoppers and make their user profiles using browser cookies. To enable this event we just need to add Unbxd’s analytics JS library (as done above) inside the head section of all pages of the site.

NOTE: The visitor event will be fired from the SDK itself. If you have integrated the Unbxd analytics JS code, this event is tracked and pushed automatically, with no further action required.

The Visitor event is the first event that gets created when a shopper visits your site.  There are two types of shoppers we track:

* First-time shoppers
* Repeat shoppers

### **Search**

The search query event should be tracked when the user performs a search on site. It even includes selecting any option from Unbxd’s Autosuggest widget. It should track the query which user used to fetch the response (even the zero result queries should be tracked).

NOTE: In case of Search SDK integration, we do not have to add this event explicitly and is handled hand in hand by the Search and Analytics SDK. Please ensure that unbxdAnalytics flag is set as “true” in Search SDK config, to allow this event to fire automatically with no further action for this event.

Use the below code as a reference to be inserted in HTML tags for input box and search button divs respectively:

1. Insert the unbxdattr=”sq” attribute within the \< input > tag of the search box to capture the search query typed by the shopper. For eg:

```
<input type="text" placeholder="Search" unbxdattr=”sq”/>
```

2. The unbxdattr=”sq\_bt” attribute is inserted on the link or search button (usually the magnification/search icon) that triggers search at the backend.

```
<button type = "submit" unbxdattr = "sq_bt" > Search </button>
```

Parameter details:

| Attribute Name | Datatype | What value to be passed                                                   |
| -------------- | -------- | ------------------------------------------------------------------------- |
| `unbxdattr`    | constant | `"sq"` in case of input `\<div>`\<br>`"sq_bt"` in case of button `\<div>` |

### Search Impression

A search impression event is fired when a search results page loads for the first time, and whenever results change on applying pagination, autoscroll, sort, and filters. For each of these actions, unique Ids of the products visible on the search page should be sent as payload.

NOTE: In case of Search SDK integration, we do not have to add this event explicitly and is handled hand in hand by the Search and Analytics SDK. Please ensure that unbxdAnalytics flag is set as “true” in Search SDK config, to allow this event to fire automatically with no further action for this event.

To track a search results page impression, insert the following HTML tag on the search product title on the results page on your site.

```
<li unbxdAttr="product" unbxdparam_sku="{{uniqueId-of-product}}">
```

Also, add the script below before Unbxd analytics library is loaded.

```
<script type="text/javascript">
UnbxdAnalyticsConf=window.UnbxdAnalyticsConf ||{};
UnbxdAnalyticsConf["query"]="{{search-query}}";
</script>
```

Parameter details:

| Attribute Name   | Datatype | What value to be passed                                                                                            |
| ---------------- | -------- | ------------------------------------------------------------------------------------------------------------------ |
| `unbxdattr`      | constant | Specifies the type of event being captured. For search results product, the value is `"product"` always.           |
| `unbxdparam_sku` | variable | Specifies the uniqueId of the product as defined in the feed. You can get this from the UNBXD search API response. |
| `query`          | variable | The search query which was called for loading the results.                                                         |

### Product Click

The Product Click event is generated every time a shopper clicks on a product in a Product Listing Page (PLP) or in a recommendation widget. This helps us understand your shoppers’ search preferences. This information is analyzed to list and promote ‘Popular Products’ in the autosuggest dropdown  and display personalized ‘Recommended For You’ recommendations.

To display products within the PLP on the search results or category page, insert the following code snippet within \<div> of product grid (product thumbnail) or within the \<li> html tag.

Sample code snippet with \<li> tags

```
<li unbxdattr="product" unbxdparam_sku="{{uniqueId-of-product}}" unbxdparam_prank="{{rank-of-product}}" unbxdparam_requestId="{{window.requestId}}"> </li>

```

Sample code snippet within \<div> tags

```
<div unbxdattr="product" unbxdparam_sku="{{uniqueId-of-product}}" unbxdparam_prank="{{rank-of-product}}" unbxdparam_requestId="{{window.requestId}}" />

Parameter details:
```

Parameter details:

| **Attribute Name**     | **Datatype** | **What value to be passed**                                                                                                                                                     |
| ---------------------- | ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `unbxdattr`            | Constant     | Specifies the type of event being captured. For product clicks, the value is “product” always.                                                                                  |
| `unbxdparam_sku`       | Variable     | Specifies the uniqueId of the product as defined in the feed. You can get this from the UNBXD search API response.                                                              |
| `unbxdparam_prank`     | Variable     | Specifies the position of the product in the search results grid/list. When this value is not specified, the first product will have a value of 1, second will be 2, and so on. |
| `unbxdparam_requestId` | Variable     | Specifies the request Id, which is part of the response readers of the Search/Category API request. For Search SDK integration, this is handled by the SDK and can be ignored.  |

Product View\
Product View indicates the total number of visits that has been made to the product details page (PDP) by the visitor irrespective of the source (search result page, category page, search engine, email, marketing campaigns, etc).The product view can be tracked whenever a user lands on the PDP page by adding the below link to your HTML on page load.

```
<li unbxdattr= “ProductView” unbxdparam_sku = “{{uniqueId-of-product}}” unbxdparam_variant = “{{variantId-of-variant}}” > </li>
```

Parameter details:

| **Attribute Name**   | **Datatype**        | **What value to be passed**                                                                                                                                        |
| -------------------- | ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `unbxdattr`          | Constant            | Specifies the type of event being captured. For product view, the value is “ProductView” always.                                                                   |
| `unbxdparam_sku`     | Variable            | Specifies the uniqueId of the product as defined in the feed. You can get this from the UNBXD search API response.                                                 |
| `unbxdparam_variant` | Variable (Optional) | Specifies the uniqueID (variantId) of the product variant added to the cart as defined in the feed schema. This parameter is required if the catalog has variants. |

Add to Cart\
Whenever a user adds any product to cart or shopping bag, the add to cart event will get fired. To track this event , insert the following code snippet on the “Add to Cart” button within your HTML page.

```
<li unbxdattr="AddToCart"  unbxdparam_sku="{{uniqueId-of-product}}" unbxdparam_variant= “{{variantId-of-variant}}” unbxdparam_qty="{{no-of-units}}" unbxdparam_requestId="{{window.requestId}}" ></li>
```

Parameter details

| **Attribute Name**     | **Datatype**         | **What value to be passed**                                                                                                                                                                                                                                                                  |
| ---------------------- | -------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `unbxdattr`            | Constant             | Specifies the type of event being captured. For the cart event, the value is “AddToCart.”                                                                                                                                                                                                    |
| `unbxdparam_sku`       | Variable             | Specifies the uniqueId of the product as defined in the feed. You can get this from the UNBXD search API response.                                                                                                                                                                           |
| `unbxdparam_variant`   | Variable (Optional)  | Specifies the uniqueID of the product variant added to the cart as defined in the feed schema. This parameter is required if the catalog has variants.                                                                                                                                       |
| `unbxdparam_qty`       | Variable (Mandatory) | The number of units added to the cart. This should be the string value of the quantity added. For example, if 4 quantities of a product are added, its value would be “4” (instead of 4).                                                                                                    |
| `unbxdparam_requestId` | Variable             | Specifies the request Id from the response of the search/category API. If the widget is not on the listing page, this parameter can be ignored when products within the PLP widget have the "Add to Cart" button. For Search SDK integration, this is handled by the SDK and can be ignored. |

Cart Removal\
This event tracks every instance a product is removed from cart as well. Information helps us better understand the visitor’s preferences. To track products being removed from cart, insert the following attributes within all “Remove from Cart” buttons on the cart page.

```
<button unbxdattr= “RemoveFromcart” unbxdparam_sku= “{{uniqueId-of-product}}” unbxdparam_variant = “{{variantId-of-product}}” unbxdparam_price = “{{price-of-product}}” unbxdparam_qty = “{{no-of-units}}”/></button>
```

| **Attribute Name**   | **Datatype**         | **What value to be passed**                                                                                                                                                                       |
| -------------------- | -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `unbxdattr`          | Constant             | Specifies the type of event being captured. For cart removal, the value is “RemoveFromCart.”                                                                                                      |
| `unbxdparam_sku`     | Variable             | Specifies the uniqueId of the product as defined in the feed. You can get this from the UNBXD search API response.                                                                                |
| `unbxdparam_variant` | Variable (Optional)  | Specifies the uniqueID of the product variant removed from the cart as defined in the feed schema. This parameter is required if the catalog has variants.                                        |
| `unbxdparam_price`   | Variable             | Specifies the price of the individual product/variant removed from the cart.                                                                                                                      |
| `unbxdparam_qty`     | Variable (Mandatory) | The number of units removed from the cart. This should be the string value of the quantity removed. For example, if 4 quantities of a product are removed, its value would be “4” (instead of 4). |

Order\
The Orders event is pushed for every product that is purchased on your site.

Using Custom HTML attributes you can integrate the functionality to track orders that have been successfully completed.

You can insert the following code snippet within \< div > of product grid (product thumbnail) or within the \< li > html tag.To display products within the PLP on the search results:

```
<li unbxdattr="order"  unbxdparam_sku="{{uniqueId-of-product}}" unbxdparam_variant= “{{variantId-of-variant}}” unbxdparam_qty="{{no-of-units}}" unbxdparam_price=“{{price-of-product}}”></li>
```

Parameter details:

| **Attribute Name**   | **Datatype**        | **What value to be passed**                                                                                                                    |
| -------------------- | ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| `unbxdattr`          | Constant            | Specifies the type of event being captured. For product clicks, the value is “order” always.                                                   |
| `unbxdparam_sku`     | Variable            | Specifies the uniqueId of the product as defined in the feed. You can get this from the UNBXD search API response.                             |
| `unbxdparam_variant` | Variable (Optional) | Specifies the uniqueID of the product variant purchased as defined in the feed schema. This parameter is required if the catalog has variants. |
| `unbxdparam_qty`     | Variable            | Specifies the number of products/variants purchased.                                                                                           |
| `unbxdparam_price`   | Variable            | Specifies the amount of a single unit the shopper has paid for the product/variant.                                                            |