---
title: GTM Integration
deprecated: false
hidden: false
metadata:
  robots: index
---
Google Tag Manager (GTM) simplifies the process of managing and deploying tags on your website. It acts as a bridge, allowing data from your website to flow seamlessly into other data sources like Google Analytics. GTM is particularly useful when managing multiple tags, as it consolidates all the code in one centralized location, making updates and maintenance easier and more efficient.

## How to implement Analytics integration using GTM?

Add the following `<script>` tag at the end of your site's HTML body.

```html
<script   
src="https://libraries.unbxdapi.com/sdk-clients/PROD_SITEKEY/ua/ua.js">
</script>
```

Initialize the GTM window object on page load if it is not already present, using the respective `ContainerID` and `HTMLId`.

```html
/ Container ID is present in GTM-XXXX format in the GTM Dashboard
 // HTML ID can be found in the URL. Eg:
 // containers/422XXXX/workspaces/20, 20 is the HTML ID

 <script type="text/javascript">
     window.google_tag_manager[{{Container ID }}].onHtmlSuccess({{ HTML ID }}); });
 </script>
```

## Import Unbxd Template on GTM

1. [Download the JSON template](https://d29240o5wkzuh9.cloudfront.net/GTM-5GJ8NTD_workspace2.json) for Tags, Triggers, and Variables.
2. After downloading the JSON template, follow the steps in this document to import it into your GTM container.

Follow the steps below for each event to set up the `dataLayer`.

## How to track each event?

#### Search

To track each search query effectively for per-query analytics, ensure that the dataLayer event is pushed whenever a search is initiated, either by submitting a form or clicking a search button. Below is the Vanilla JavaScript implementation to handle this requirement.

Payload details:

| **Attribute Name** | **Datatype** | **What Value to Be Passed**            |
| ------------------ | ------------ | -------------------------------------- |
| `query`            | `string`     | The search query input by the shopper. |

Refer to the following code snippet:

```javascript
<script type="text/javascript">
 function handleSearchQuery() {
   var searchQuery = document.getElementById('myInput').value;
   if (searchQuery.length >= 1) {
     window.dataLayer = window.dataLayer || [];
     dataLayer.push({
       'event': 'SearchQuery',
       'SearchQueryPayload': {
         'query': searchQuery
       }
     });
   }
 }
 document.getElementById('input_form_id').addEventListener('submit', function(event) {
   handleSearchQuery();
 });
 document.getElementById('myButton').addEventListener('click', function(event) {
   handleSearchQuery();
 });
</script>
```

#### Category Page

To trigger a categoryPage event on all category (browse) pages, push the event to the dataLayer whenever a user accesses a category page.

Payload details:

| **Attribute Name** | **Datatype** | **What Value to Be Passed**                                                             |
| ------------------ | ------------ | --------------------------------------------------------------------------------------- |
| `page`             | `string`     | Category path used for the category API call (value of the `p` parameter).              |
| `page_type`        | `string`     | Page type for the category path, either `BOOLEAN` or `CATEGORY_PATH` based on the page. |

Refer to the following code snippet:

```javascript
<script type="text/javascript">
  window.onload = function() {
      window.dataLayer = window.dataLayer || [];
      dataLayer.push(
          {
              'event': 'CategoryPage',
              'CategoryPagePayload':
              {
                  'page': '{{category-path}}',
                  'page_type': '{{category-page-type}}'
              }
          }
      );
  };
</script>
```

#### Search Impression

Impression events should be tracked each time a new set of results is loaded on the search listing page.

Payload details:

| **Attribute Name** | **Datatype** | **What Value to Be Passed**                                                                                          |
| ------------------ | ------------ | -------------------------------------------------------------------------------------------------------------------- |
| `pids_list`        | `array`      | List of unique IDs of products loaded for a search query. If zero products are returned, pass an empty list (array). |
| `query`            | `string`     | Search query for the search listing page.                                                                            |

Code snippet to call the UnbxdSearchImpression tag from data layer push:

```javascript
<script type="text/javascript">
function handleSearchQuery() {
  var searchQuery = document.getElementById('myInput').value;
  if (searchQuery.length >= 1) {
    window.dataLayer = window.dataLayer || [];
    dataLayer.push({
      'event': 'SearchImpression',
      'SearchQueryPayload': {
         'pids_list': [ {{list-of-products-uniqueId}}, "352343", "1341234", "2342341", "..."],
        'query': searchQuery
      }
    });
  }
}
document.getElementById('input_form_id').addEventListener('submit', function(event) {
  handleSearchQuery();
});
document.getElementById('myButton').addEventListener('click', function(event) {
  handleSearchQuery();
});
</script>
```

#### Browse Impression

A browse impression event is triggered when category results load for the first time and whenever the results change due to pagination, autoscroll, sorting, or applying filters. For each of these actions, the unique IDs of the products displayed on the category page should be included in the payload.

Payload details:

| **Attribute Name** | **Datatype** | **What Value to Be Passed**                                                                                                |
| ------------------ | ------------ | -------------------------------------------------------------------------------------------------------------------------- |
| `pids_list`        | `array`      | List of unique IDs of products loaded with the current request. If zero products are returned, pass an empty list (array). |
| `page`             | `string`     | Category path used for the category API call (value of the `p` parameter).                                                 |
| `page_type`        | `string`     | Page type for the category path, either `BOOLEAN` or `CATEGORY_PATH` based on the page.                                    |

Code snippet to call the Unbxd BrowseImpression tag from data layer push:

```javascript
 <script type="text/javascript">
 window.onload = function() {
     window.dataLayer = window.dataLayer || [];
     dataLayer.push(
         {
             'event': 'BrowseImpression',
             'CategoryPagePayload':
             {
                 'pids_list': [ {{list-of-products-uniqueId}}, "352343", "1341234", "2342341", "..."],
                 'page': '{{category-path}}',
                 'page_type': '{{category-page-type}}'
             }
         }
     );
 };
 </script>
```

#### Search Facets

A Facet event tracks the guided navigation on the Product Listing Page. The event query will list the specific filters the shopper has selected to narrow down the results on the search results page.

Payload details:

| **Attribute Name** | **Datatype** | **What Value to Be Passed**                                                          |
| ------------------ | ------------ | ------------------------------------------------------------------------------------ |
| `facets`           | `object`     | Should contain key-value pairs of selected facet names and lists of selected values. |
| `query`            | `string`     | Search query for the search listing page.                                            |

Code snippet for Selection and Deselection of facets:

```javascript
<script type="text/javascript">
function handleSearchQuery() {
  var searchQuery = document.getElementById('myInputBox').value;
  if (searchQuery.length >= 1) {
    window.dataLayer = window.dataLayer || [];
    dataLayer.push({
      'event': 'SearchFacets',
      'SearchFacetsPayload': {
         'facets': {'facet_name1': {'prank': '1','selected':[{'prank': '2', 'val': 'facet_value1'},{'prank': '3','val': 'facet_value2'}]}, 'facet_name2': {'prank': '2', 'deselected':[{'prank': '1','val': 'facet_value1'},{'prank': '5','val': 'facet_value2'}]} }
         'query': searchQuery
      }
    });
  }
}
</script>
```

Code snippet for Clear All  facets:

```javascript
<script type="text/javascript">
function handleSearchQuery() {
 var searchQuery = document.getElementById('myInput').value;
 if (searchQuery.length >= 1) {
   window.dataLayer = window.dataLayer || [];
   dataLayer.push({
     'event': 'SearchFacets',
     'SearchFacetsPayload': {
        'facets': {'unxFacetsReset': true}
        'query': searchQuery
     }
   });
 }
}
</script>
```

#### Browse Facets

A Facet event monitors the guided navigation on Category and Browse Pages, capturing the specific filters the shopper has chosen to refine the results displayed on the browse results page.

Payload details:

| **Attribute Name** | **Datatype** | **What Value to Be Passed**                                                             |
| ------------------ | ------------ | --------------------------------------------------------------------------------------- |
| `facets`           | `object`     | Should contain key-value pairs of selected facet names and lists of selected values.    |
| `page`             | `string`     | Category path used for the category API call (value of the `p` parameter).              |
| `page_type`        | `string`     | Page type for the category path, either `BOOLEAN` or `CATEGORY_PATH` based on the page. |

Code snippet to call the Unbxd BrowseFacets tag from data layer push:

```javascript
<script type="text/javascript">
 window.dataLayer = window.dataLayer || [];
 dataLayer.push({
   'event': 'BrowseFacets',
   'BrowseFacetsPayload': {
       'facets': {'facet_name1': {'prank': '1','selected':[{'prank': '2', 'val': 'facet_value1'},{'prank': '3','val': 'facet_value2'}]}, 'facet_name2': {'prank': '2', 'deselected':[{'prank': '1','val': 'facet_value1'},{'prank': '5','val': 'facet_value2'}]} }
       'page': '{{category-path}}',
       'page_type': '{{category-page-type}}',


   }
 });
</script>
```

Code snippet for Clear All facets

```javascript
<script type="text/javascript">
window.dataLayer = window.dataLayer || [];
dataLayer.push({
  'event': 'BrowseFacets',
  'BrowseFacetsPayload': {
      'facets': {'unxFacetsReset': true}
      'page': '{{category-path}}',
      'page_type': '{{category-page-type}}',
  }
});
</script>
```

#### Click

The click event must be recorded whenever a user clicks on a product to access its details page. This tracking applies to both the Search Results Page (SRP) and the Category Results Page (CRP), depending on the Unbxd service you have selected.

Payload details:

| **Attribute Name** | **Datatype** | **What Value to Be Passed**                                          |
| ------------------ | ------------ | -------------------------------------------------------------------- |
| `pid`              | `string`     | Unique ID for the product, to be taken from the Search API response. |

Refer to the following code snippet:

```javascript
<script type="text/javascript">
 document.getElementById('.product-div').addEventListener('click', function() {
     window.dataLayer = window.dataLayer || [];
     dataLayer.push({
         'event': 'ProductClick',
         'ProductClickPayload': {
             'pid': '{{unique-id}}'
         }
     });
 });
</script>
```

#### Cart

The cart event should be monitored when a user adds a product to their cart or modifies an existing carted product. This event must be implemented wherever users have the option to add or modify items in their cart.

Payload details:

| **Attribute Name** | **Datatype** | **Value to Be Passed**                                        |
| ------------------ | ------------ | ------------------------------------------------------------- |
| `pid`              | `string`     | Unique ID for the product, to be taken from the API response. |
| `variantId`        | `string`     | The variant ID of the selected product variant.               |
| `qty`              | `string`     | Quantity being added to the cart by the user.                 |

Refer to the following code snippet:

```javascript
<button id="add-to-cart-button">Add to Cart</button>
<script type="text/javascript">
   document.getElementById('add-to-cart-button').addEventListener('click', function() {
       window.dataLayer = window.dataLayer || [];
       dataLayer.push({
           'event': 'ProductCarted',
           'ProductCartedPayload': {
               'pid': 'PRODUCT ID',
               'variantId': 'VARIANT ID OF SELECTED VARIANT',
               'qty': 'QUANTITY SELECTED',
           }
       });
   });
</script>
```

#### Order

The order event is best tracked on the order-success page. The script below leverages the Unbxd.trackMultiple analytics interface API, which allows for the inclusion of one or more products in the payload to trigger the event.

Payload details:

| **Attribute Name** | **Datatype** | **What Value to Be Passed**                                          |
| ------------------ | ------------ | -------------------------------------------------------------------- |
| `pid`              | `string`     | Unique ID for the product, to be taken from the Search API response. |
| `variantId`        | `string`     | Variant ID of the selected product variant.                          |
| `qty`              | `string`     | Quantity being added by the user.                                    |
| `price`            | `string`     | Unit price of the product.                                           |

Refer to the following code snippet:

```javascript
script type="text/javascript">
 window.addEventListener('load', function() {
     window.dataLayer = window.dataLayer || [];
     dataLayer.push({
         'event': 'ProductOrder',
         'ProductsOrderedPayload': [{
                 'pid': '{{uniqueId-of-product1}}',
                 'variantId': '{{variantId-of-product1}}',
                 'qty': 'QUANTITY SELECTED 1',
		    'price': '{{unit-price-for-product}}',


             },
             {
                 'pid': '{{uniqueId-of-product2}}',
                 'variantId': '{{variantId-of-product2}}',
                 'qty': 'QUANTITY SELECTED 2',
                 'price': '{{unit-price-for-product}}',
             }
         ]
     });
 });
</script>
```

### Autosuggest

When a user selects and submits a suggestion from the Autosuggest widget, the respective event should be captured and sent with additional metadata (autosuggestParams).

For Google Tag Manager (GTM) implementation, whenever a suggestion is selected from the Autosuggest box, the following events should be fired, sending relevant metadata in the payload.

#### KEYWORD\_SUGGESTION

Payload details:

| **Attribute Name**       | **Datatype** | **What Value to Be Passed**                                                                          |
| ------------------------ | ------------ | ---------------------------------------------------------------------------------------------------- |
| `autosuggest_type`       | `string`     | `KEYWORD_SUGGESTION`, usually the same as the value of the `doctype` field in Unbxd autosuggest API. |
| `autosuggest_suggestion` | `string`     | Suggested query in keyword.                                                                          |
| `field_name`             | `string`     | In case of `KEYWORD` suggestions, the name of the field used for the suggestion.                     |
| `field_value`            | `string`     | In case of `KEYWORD` suggestions, the value of the field, which is the suggestion.                   |
| `src_field`              | `string`     | Source field, can be passed empty.                                                                   |
| `internal_query`         | `string`     | The typed query in the search box, which led to the suggestions in autosuggest.                      |

```javascript
Refer to the following code snippet:
<script type="text/javascript">
   document.getElementById('input_form_id').addEventListener('submit', function(event) {
   var searchQuery = document.getElementById('myInput').value;
   if (searchQuery.length >= 1) {
       window.dataLayer = window.dataLayer || [];
       window.dataLayer.push({
           'event': 'AutosuggestSearchTrigger',
           'AutosuggestSearchPayload':{
               'query': '{{suggested-query}}',
               'autosuggestParams': {
                   'autosuggest_type': 'KEYWORD_SUGGESTION',
                   'autosuggest_suggestion': '{{suggestion}}',
             'unbxdprank': '{{rank-of-product}}',
                   'internal_query': '{{original-query}}'
               }
             }
       });
   }
   });
</script>
```

#### IN\_FIELD

Payload details:

| **Attribute Name**       | **Datatype** | **What Value to Be Passed**                                                                |
| ------------------------ | ------------ | ------------------------------------------------------------------------------------------ |
| `query`                  | `string`     | Suggested query in Infield.                                                                |
| `autosuggest_type`       | `string`     | `IN_FIELD`, usually the same as the value of the `doctype` field in Unbxd autosuggest API. |
| `autosuggest_suggestion` | `string`     | Suggested query in `IN_FIELD` that is selected.                                            |
| `src_field`              | `string`     | Source field, can be passed empty.                                                         |
| `field_name`             | `string`     | In case of `IN_FIELD` suggestions, the name of the field used for the suggestion.          |
| `field_value`            | `string`     | In case of `IN_FIELD` suggestions, the value of the field, which is the suggestion.        |
| `internal_query`         | `string`     | The typed query in the search box, which led to the suggestions in autosuggest.            |

Refer to the following code snippet:

```javascript
<script type="text/javascript">
   document.getElementById('input_form_id').addEventListener('submit', function(event) {
   var searchQuery = document.getElementById('myInput').value;
   if (searchQuery.length >= 1) {
       window.dataLayer = window.dataLayer || [];
       window.dataLayer.push({
           'event': 'AutosuggestSearchTrigger',
           'AutosuggestSearchPayload': {
               'query': '{{suggested-query}}',
               'autosuggestParams': {
                   'autosuggest_type': 'IN_FIELD',
                   'autosuggest_suggestion': '{{suggestion}}',
                   'field_name': '{{infield-name}}',
                   'field_value': '{{infield-value}}',
                   'src_field': '{{src-field-name}}',
                   'internal_query': '{{original-query}}'
               }
           }
       });
   }
   });
</script>
```

#### TOP\_SEARCH\_QUERIES

Payload details:

| **Attribute Name**       | **Datatype** | **What Value to Be Passed**                                                                                                              |
| ------------------------ | ------------ | ---------------------------------------------------------------------------------------------------------------------------------------- |
| `autosuggest_type`       | `string`     | `TOP_SEARCH_QUERIES` depending on the type of suggestion, usually the same as the value of the `doctype` field in Unbxd autosuggest API. |
| `autosuggest_suggestion` | `string`     | Suggested query in Infield.                                                                                                              |
| `internal_query`         | `string`     | The typed query in the search box, which led to the suggestions in autosuggest.                                                          |
| `unbxdprank`             | `string`     | In case of `POPULAR_PRODUCTS` suggestions, the rank of the product.                                                                      |

Refer to the following code snippet:

```javascript
<script type="text/javascript">
   document.getElementById('input_form_id').addEventListener('submit', function(event) {
   var searchQuery = document.getElementById('myInput').value;
   if (searchQuery.length >= 1) {
       window.dataLayer = window.dataLayer || [];
       window.dataLayer.push({
           'event': 'AutosuggestSearchTrigger',
           'AutosuggestSearchPayload':{
               'query': '{{suggested-query}}',
               'autosuggestParams': {
                   'autosuggest_type': 'TOP_SEARCH_QUERIES',
                   'autosuggest_suggestion': '{{suggestion}}',
                   'internal_query': '{{original-query}}',
            'unbxdprank': '{{rank-of-product}}',
               }
             }
       });
   }
   });
</script>
```

#### PROMOTED\_SUGGESTION

Payload details:

| **Attribute Name**       | **Datatype** | **What Value to Be Passed**                                                                                                               |
| ------------------------ | ------------ | ----------------------------------------------------------------------------------------------------------------------------------------- |
| `autosuggest_type`       | `string`     | `PROMOTED_SUGGESTION` depending on the type of suggestion, usually the same as the value of the `doctype` field in Unbxd autosuggest API. |
| `autosuggest_suggestion` | `string`     | Suggested query in Infield.                                                                                                               |
| `internal_query`         | `string`     | The typed query in the search box, which led to the suggestions in autosuggest.                                                           |
| `unbxdprank`             | `string`     | In case of `POPULAR_PRODUCTS` suggestions, the rank of the product.                                                                       |

Refer to the following code snippet:

```javascript
<script type="text/javascript">
  document.getElementById('input_form_id').addEventListener('submit', function(event) {
  var searchQuery = document.getElementById('myInput').value;
  if (searchQuery.length >= 1) {
      window.dataLayer = window.dataLayer || [];
      window.dataLayer.push({
          'event': 'AutosuggestSearchTrigger',
          'AutosuggestSearchPayload':{
              'query': '{{suggested-query}}',
              'autosuggestParams': {
                  'autosuggest_type': 'PROMOTED_SUGGESTION',
                  'autosuggest_suggestion': '{{suggestion}}',
                  'internal_query': '{{original-query}}',
                  'unbxdprank': '{{rank-of-product}}',
              }
            }
      });
  }
  });
</script>
```

#### TRENDING\_QUERIES

Payload details:

| **Attribute Name**       | **Datatype** | **What Value to Be Passed**                                                                                                              |
| ------------------------ | ------------ | ---------------------------------------------------------------------------------------------------------------------------------------- |
| `autosuggest_type`       | `string`     | `TOP_SEARCH_QUERIES` depending on the type of suggestion, usually the same as the value of the `doctype` field in Unbxd autosuggest API. |
| `autosuggest_suggestion` | `string`     | Suggested query in Infield.                                                                                                              |
| `internal_query`         | `string`     | The typed query in the search box, which led to the suggestions in autosuggest.                                                          |
| `unbxdprank`             | `string`     | In case of `POPULAR_PRODUCTS` suggestions, the rank of the product.                                                                      |
| `misc`                   | `object`     | A special object used to pass additional data along the event.                                                                           |
| `unxAsType`              | `string`     | This attribute goes into the `misc` object to indicate this is a type of `TRENDING_QUERIES`.                                             |

Refer to the following code snippet:

```javascript
<script type="text/javascript">
  document.getElementById('input_form_id').addEventListener('submit', function(event) {
  var searchQuery = document.getElementById('myInput').value;
  if (searchQuery.length >= 1) {
      window.dataLayer = window.dataLayer || [];
      window.dataLayer.push({
          'event': 'AutosuggestSearchTrigger',




          'AutosuggestSearchPayload':{
              'query': '{{suggested-query}}',
              'misc': {
                   'unxAsType':'TRENDING_QUERIES',
              }
              'autosuggestParams': {
                  'autosuggest_type': 'TOP_SEARCH_QUERIES',
                  'autosuggest_suggestion': '{{suggestion}}',
                  'internal_query': '{{original-query}}',
                  'unbxdprank': '{{rank-of-product}}',
              }
            }
      });
  }
  });
</script>
```

#### FIELD\_TYPE\_SUGGESTION

Payload details:

| **Attribute Name**       | **Datatype** | **What Value to Be Passed**                                                                                                                                             |
| ------------------------ | ------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `autosuggest_type`       | `string`     | `KEYWORD_SUGGESTION` depending on the type of suggestion, usually the same as the value of the `doctype` field in Unbxd autosuggest API.                                |
| `autosuggest_suggestion` | `string`     | Suggested query in Infield.                                                                                                                                             |
| `unbxdprank`             | `string`     | In case of `POPULAR_PRODUCTS` suggestions, the rank of the product.                                                                                                     |
| `internal_query`         | `string`     | The typed query in the search box, which led to the suggestions in autosuggest.                                                                                         |
| `misc`                   | `object`     | A special object used to pass additional data along the event.                                                                                                          |
| `unxAsType`              | `string`     | This attribute goes into the `misc` object to indicate this is a type of `FIELD_TYPE_SUGGESTION`.                                                                       |
| `unxAsFieldName`         | `string`     | This attribute goes into the `misc` object to indicate the `field` on which the `FIELD_TYPE_SUGGESTION` has been set up. The value can be the field name from the feed. |

Refer to the following code snippet:

```javascript
<script type="text/javascript">
  document.getElementById('input_form_id').addEventListener('submit', function(event) {
  var searchQuery = document.getElementById('myInput').value;
  if (searchQuery.length >= 1) {
      window.dataLayer = window.dataLayer || [];
      window.dataLayer.push({
          'event': 'AutosuggestSearchTrigger',




          'AutosuggestSearchPayload':{
              'query': '{{suggested-query}}',
              'misc': {
                   'unxAsType':'FIELD_TYPE_SUGGESTION',
                   'unxAsFieldName': 'Brand'
              }
              'autosuggestParams': {
                  'autosuggest_type': 'KEYWORD_SUGGESTION',
                  'autosuggest_suggestion': '{{suggestion}}',
                  'internal_query': '{{original-query}}',
                  'unbxdprank': '{{rank-of-product}}',
              }
            }
      });
  }
  });
</script>
```

#### POPULAR\_PRODUCTS

Payload details:

| **Attribute Name** | **Datatype** | **What Value to Be Passed**                                                                        |
| ------------------ | ------------ | -------------------------------------------------------------------------------------------------- |
| `query`            | `string`     | Title of the product.                                                                              |
| `autosuggest_type` | `string`     | `POPULAR_PRODUCTS`, usually the same as the value of the `doctype` field in Unbxd autosuggest API. |
| `pid`              | `string`     | Unique ID of the selected popular product.                                                         |
| `unbxdprank`       | `string`     | In case of `POPULAR_PRODUCTS` suggestions, the rank of the product.                                |
| `internal_query`   | `string`     | The typed query in the search box, which led to the suggestions in autosuggest.                    |

Refer to the following code snippet:

```javascript
<script type="text/javascript">
   document.getElementById('input_form_id').addEventListener('submit', function(event) {
   var searchQuery = document.getElementById('myInput').value;
   if (searchQuery.length >= 1) {
       window.dataLayer = window.dataLayer || [];
       window.dataLayer.push({
           'event': 'AutosuggestSearchTrigger',
           'AutosuggestSearchPayload':{
               'query': '{{title-of-product}}',
               'autosuggestParams': {
                'autosuggest_type': 'POPULAR_PRODUCTS',
                'pid': '{{uniqueId-of-the-product}}',
                'unbxdprank': '{{rank-of-product}}',
                'internal_query': '{{original-query}}'
               }
             }
       });
   }
   });
</script>
```

#### POPULAR\_PRODUCTS\_FILTERED

Payload details:

| **Attribute Name**       | **Datatype** | **What Value to Be Passed**                                                                                                                     |
| ------------------------ | ------------ | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| `query`                  | `string`     | Title of the product.                                                                                                                           |
| `autosuggest_type`       | `string`     | `POPULAR_PRODUCTS_FILTERED` depending on the type of suggestion, usually the same as the value of the `doctype` field in Unbxd autosuggest API. |
| `autosuggest_suggestion` | `string`     | Suggested query in Infield.                                                                                                                     |
| `internal_query`         | `string`     | The typed query in the search box, which led to the suggestions in autosuggest.                                                                 |
| `unbxdprank`             | `string`     | In case of `POPULAR_PRODUCTS` suggestions, the rank of the product.                                                                             |

Refer to the following code snippet:

```javascript
<script type="text/javascript">
   document.getElementById('input_form_id').addEventListener('submit', function(event) {
   var searchQuery = document.getElementById('myInput').value;
   if (searchQuery.length >= 1) {
       window.dataLayer = window.dataLayer || [];
       window.dataLayer.push({
           'event': 'AutosuggestSearchTrigger',
           'AutosuggestSearchPayload':{
               'query': '{{suggested-query}}',
               'autosuggestParams': {
                   'autosuggest_type': 'POPULAR_PRODUCTS_FILTERED',
                   'autosuggest_suggestion': '{{suggestion}}',
                   'internal_query': '{{original-query}}',
            'unbxdprank': '{{rank-of-product}}',
               }
             }
       });
   }
   });
</script>
```