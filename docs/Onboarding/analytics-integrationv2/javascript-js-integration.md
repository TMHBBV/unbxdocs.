---
title: JavaScript (JS) Integration
deprecated: false
hidden: false
metadata:
  robots: index
---
> 📘 Note
>
> This method should primarily be used when the client prefers to manage the process directly or if the event integration has failed through other recommended approaches.

The Unbxd Search JS Library is an SDK for adding search and product discovery features to e-commerce websites. It is written in Vanilla JavaScript and provides a JavaScript API for configuring and managing search requests.

The SDK has no external dependencies, making it lightweight and straightforward to integrate. To use it, a script tag is added to the relevant webpage. Developers can customize and extend its functionality through JavaScript methods and callbacks.

# How to do the JS-based Analytics integration?

Add the following `<script>` tag at the end of your site's HTML body.

```
<script type="text/javascript" defer charset="utf-8"
  src="https://libraries.unbxdapi.com/sdk-clients/PROD_SITEKEY/ua/ua.js">
</script>
```

# What are the event payload data required?

## Search

This tracks user search queries, including those using the Autosuggest widget. It is important to capture all search queries, including ones with zero results.

### Payload details

| Attribute Name | Type   | Value to Pass                            |
| :------------- | :----- | :--------------------------------------- |
| `query`        | String | The search query entered by the shopper. |

Refer to the following code snippet to call the Unbxd.track function to trigger the search event.

```
 <script type="text/javascript">
   	var payload = {
   	query: '{{search-query}}',
   	}


   	if(Unbxd && typeof Unbxd.track === 'function') {
   		Unbxd.track('search', payload)
   	} else {
   		console.error('unbxdAnalytics.js is not loaded!')
   	}
   </script>
```

# Visual Search

## Payload details

| Attribute Name | Datatype | What Value to be Passed                                                                                                 |
| :------------- | :------- | :---------------------------------------------------------------------------------------------------------------------- |
| `imageId`      | String   | Id of the image, to be retrieved from the response of visualSearch API                                                  |
| `boxId`        | String   | Optional, the ID of the bounding box that has been selected. Look for the selected key in the visualSearch API response |

Refer to the following code snippet to call the `Unbxd.track` function to trigger the `visualSearch` event.

```
<script type="text/javascript">
   	var payload = {
   	imageId: 'ad85491c-9d2b-4cab-900a-df96aa11f0d9',
     	boxId: '1089',
   	}


   	if(Unbxd && typeof Unbxd.track === 'function') {
   		Unbxd.track('visualSearch', payload)
   	} else {
   		console.error('unbxdAnalytics.js is not loaded!')
   	}
   </script>
```

# Category Page

To be triggered on all category pages of the e-commerce site.

## Payload details

| Attribute Name | Datatype | What Value to Be Passed                                                             |
| :------------- | :------- | :---------------------------------------------------------------------------------- |
| `page`         | String   | Category path used for category API call (value of the p parameter).                |
| `page_type`    | String   | Page type for category path, either `BOOLEAN` or `CATEGORY_PATH` based on the page. |

Refer to the following code snippet to call the `Unbxd.track` function to trigger the categoryPage event:

```
<script type="text/javascript">
       var payload = {
           page: '{{ category- path}}',
           page_type: '{{ category- page - type}}'
       }
       if(Unbxd && typeof Unbxd.track === 'function') {
           Unbxd.track('categoryPage', payload)
       } else {
           console.error('unbxdAnalytics.js is not loaded!')
       }
   </script>
```
#### Search Impression

Should be tracked each time a new set of results is loaded on the search listing page. This ensures that all product impressions are properly recorded as users interact with the search results.

Payload details:
| **Attribute Name** | **Datatype** | **What Value to Be Passed**                                                                |
|---------------------|-------------|--------------------------------------------------------------------------------------------|
| `pids_list`        | `array`     | List of unique IDs of products loaded for a search query. If zero products are returned, pass an empty list (array). |
| `query`            | `string`    | Search query for the search listing page.                                                  |

Refer to the following code snippet:

```html
<script type="text/javascript">
   var payload = {
     pids_list: [ {{list-of-products-uniqueId}}, "352343", "1341234", "2342341", "..."],
     query: '{{search-query}}',
   }
   var action = 'search_impression'
   if(Unbxd && typeof Unbxd.track === 'function') {
     Unbxd.track(action, payload)
   } else {
     console.error('unbxdAnalytics.js is not loaded!')
   }
 </script>
```

#### Browse Impression

Triggered when category results are loaded for the first time, as well as when results change due to pagination, autoscroll, sorting, or filtering. For each of these actions, the unique IDs of the products visible on the category page should be included in the payload.

Payload details:
| **Attribute Name** | **Datatype** | **What Value to Be Passed**                                                                |
|---------------------|-------------|--------------------------------------------------------------------------------------------|
| `pids_list`        | `array`     | List of unique IDs of products loaded with the current request. If zero products are returned, pass an empty list (array). |
| `page`             | `string`    | Category path used for the category API call (value of the `p` parameter).                 |
| `page_type`        | `string`    | Page type for the category path, either `BOOLEAN` or `CATEGORY_PATH` based on the page.    |

Refer to the following code snippet:

```html
<script type="text/javascript">
   var payload = {
     pids_list: [ {{list-of-products-uniqueId}}, "352343", "1341234", "2342341", "..."],
     page: '{{category-path}}',
     page_type: '{{category-page-type}}',
   }
   var action = 'browse_impression'
   if(Unbxd && typeof Unbxd.track === 'function') {
     Unbxd.track(action, payload)
   } else {
     console.error('unbxdAnalytics.js is not loaded!')
   }
 </script>
```

#### Search Facets

This will track and log the specific filters selected by the shopper to narrow down the results on the search results page.

Payload details:
| **Attribute Name** | **Datatype** | **What Value to Be Passed**                                                                 |
|---------------------|-------------|---------------------------------------------------------------------------------------------|
| `facets`           | `object`    | Should contain key-value pairs of selected facet names and a list of selected values.        |
| `query`            | `string`    | Search query for the search listing page.                                                   |

Refer to the following code snippet for Selection and Deselection of Facets:

```html
<script type="text/javascript">
   var payload = {
     query: '{{search-query}}',
     facets: {'facet_name1': {'prank': '1','selected':[{'prank': '2', 'val': 'facet_value1'},{'prank': '3','val': 'facet_value2'}]}, 'facet_name2': {'prank': '2', 'deselected':[{'prank': '1','val': 'facet_value1'},{'prank': '5','val': 'facet_value2'}]} }
   }
   if(Unbxd && typeof Unbxd.track === 'function') {
     Unbxd.track('facets', payload)
   } else {
     console.error('unbxdAnalytics.js is not loaded!')
   }
 </script>
```

Refer to the following code snippet for Clear All Facets:

```html
<script type="text/javascript">
   var payload = {
     query: '{{search-query}}',
     facets: {'unxFacetsReset': true}
   }
   if(Unbxd && typeof Unbxd.track === 'function') {
     Unbxd.track('facets', payload)
   } else {
     console.error('unbxdAnalytics.js is not loaded!')
   }
 </script>
```

#### Browse Facets

This will track and log the specific filters selected by the shopper to narrow down the results on the category pages.

Payload details:
| **Attribute Name** | **Datatype** | **What Value to Be Passed**                                                                |
|---------------------|-------------|--------------------------------------------------------------------------------------------|
| `facets`           | `object`    | Should contain key-value pairs of selected facet names and a list of selected values.       |
| `page`             | `string`    | Category path used for the category API call (value of the `p` parameter).                 |
| `page_type`        | `string`    | Page type for the category path, either `BOOLEAN` or `CATEGORY_PATH` based on the page.    |

Refer to the following code snippet to call Unbxd’s track method:

```html
<script type="text/javascript">
   var payload = {
     page: '{{category-path}}',
     page_type: '{{category-page-type}}',
     facets: {'facet_name1': {'prank': '1','selected':[{'prank': '2', 'val': 'facet_value1'},{'prank': '3','val': 'facet_value2'}]}, 'facet_name2': {'prank': '2', 'deselected':[{'prank': '1','val': 'facet_value1'},{'prank': '5','val': 'facet_value2'}]} }
   }
   if(Unbxd && typeof Unbxd.track === 'function') {
     Unbxd.track('facets', payload)
   } else {
     console.error('unbxdAnalytics.js is not loaded!')
   }
 </script>
```

Refer to the following code snippet for Clear All Facets:

```html
<script type="text/javascript">
   var payload = {
     page: '{{category-path}}',
     page_type: '{{category-page-type}}',
     facets: {'unxFacetsReset': true}
   }
   if(Unbxd && typeof Unbxd.track === 'function') {
     Unbxd.track('facets', payload)
   } else {
     console.error('unbxdAnalytics.js is not loaded!')
   }
 </script>
```

#### Click

The click event should be tracked whenever a user clicks on a product to navigate to the product details page. This event is recorded on both the Search Results Page (SRP) and Category Results Page (CRP), depending on the Unbxd service being used.

Payload details:
| **Attribute Name** | **Datatype** | **What Value to Be Passed**                                           |
|---------------------|-------------|------------------------------------------------------------------------|
| `pid`              | `string`    | Unique ID for the product, to be taken from the Search API response.  |

Refer to the following code snippet:

```html
<script type="text/javascript">
       var payload = {
           pid: '{{unique-id}}',
       }
       if(Unbxd && typeof Unbxd.track === 'function') {
           Unbxd.track('click', payload)
       } else {
           console.error('unbxdAnalytics.js is not loaded!')
       }
</script>
```

#### Cart

Should be tracked when a user adds a product to the cart or modifies an existing carted product.

Payload details:
| **Attribute Name** | **Datatype** | **Value to Be Passed**                                               |
|---------------------|-------------|----------------------------------------------------------------------|
| `pid`              | `string`    | Unique ID for the product, to be taken from the API response.        |
| `variantId`        | `string`    | The `variantId` of the selected product variant.                     |
| `qty`              | `string`    | Quantity being added to the cart by the user.                        |

Refer to the following code snippet:

```html
<script type="text/javascript">
       var payload = {
           pid: '{{uniqueId-of-the-product}}',
           variantId: '{{variantId-of-selected-variant}}', // only if variants present
           qty: '{{quantity-selected}}',
       }
       if(Unbxd && typeof Unbxd.track === 'function') {
           Unbxd.track('addToCart', payload)
       } else {
           console.error('unbxdAnalytics.js is not loaded!')
       }
   </script>
```

#### Order

Should ideally be tracked on the order-success page.

The script below demonstrates how to use the Unbxd.trackMultiple analytics API, which allows one or more products to be passed into the payload to trigger the event.

Payload details:
| **Attribute Name** | **Datatype** | **What Value to Be Passed**                                           |
|---------------------|-------------|------------------------------------------------------------------------|
| `pid`              | `string`    | Unique ID for the product, to be taken from the Search API response.  |
| `variantId`        | `string`    | Variant ID of the selected product variant.                           |
| `qty`              | `string`    | Quantity being added by the user.                                     |
| `price`            | `string`    | Unit price of the product.                                            |

Refer to the following code snippet:

```html
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
       }]


       if(Unbxd && typeof Unbxd.track === 'function') {
           Unbxd.trackMultiple('order', payload)
       } else {
           console.error('unbxdAnalytics.js is not loaded!')
       }
   </script>
```

## Miscellaneous Data Tracking

The misc object is used to pass additional data that may not fit into standard event payloads. This data can be configured globally to apply to all events or included specifically with individual events.

#### Global Setup

To ensure that the misc data is included with all events, set the misc object under the UnbxdAnalyticsConf configuration object on the window across all pages. Below is an example of how to implement this:

```javascript
 <script type="text/javascript">
       window.UnbxdAnalyticsConf = window.UnbxdAnalyticsConf || {}
       window.UnbxdAnalyticsConf['misc'] = {
           currency: "USD",
           region: "US",
           ABCookie: "b"
       }
   </script>
```

#### Event-Specific Misc

If you prefer to pass misc data with a specific event type, you can include it directly in the payload as follows:

```javascript
 var payload = {
   	query: '{{search-query}}',
	misc: {
          currency: "USD",
          region: "US",
          ABCookie: "b"
      }
   }
```