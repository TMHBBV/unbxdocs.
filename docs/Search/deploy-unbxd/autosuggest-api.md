---
title: Autosuggest API
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

The Autosuggest feature provides query suggestions which delivers faster results to your visitors on your site. Unbxd supports autocompleting search queries and showcasing products relevant to query as they type. Usually, this feature comes in-built with the Unbxd Search, but you can also implement Unbxd Autosuggest as a standalone feature in your site. With Autosuggest, your visitors can search their intended products directly from your site’s search bar.

## Autosuggest Endpoint

With Autosuggest, your visitors can easily search products directly from your site’s search bar.

**Method**: GET

**Endpoint**: [https://search.unbxd.io/yourapikey/yoursitekey/autosuggest](https://search.unbxd.io/yourapikey/yoursitekey/autosuggest)?

**Sample Request**

To integrate Unbxd Autosuggest, you need to make the below API call to Unbxd servers:

```
https://search.unbxd.io/yourapikey/yoursitekey/autosuggest?q=<value>&version=V2&inFields.count=<value>&popularProducts.count=<value>&keywordSuggestions.count=<value>&topQueries.count=<value>&promotedSuggestion.count=<value>&popularProducts.fields=<comma separated list of fields>&variants=<true|false>&filter=<filter_query>
```

**Request Parameters**

The table below describes the different API parameters for an autosuggest API call.

| **Parameter**               | **Description**                                                                                                                                                   |
| --------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `inFields.count`            | Defines number of autosuggest results with doctype `IN_FIELD`. Default value: **2**.                                                                              |
| `popularProducts.count`     | Defines number of autosuggest results with doctype `POPULAR_PRODUCTS`. Default value: **3**.                                                                      |
| `keywordSuggestions.count`  | Defines number of autosuggest results with doctype `KEYWORD_SUGGESTION`. Default value: **2**.                                                                    |
| `topQueries.count`          | Defines number of autosuggest results with doctype `TOP_QUERIES`. Default value: **2**.                                                                           |
| `popularProducts.fields`    | Returns the fields required for popular products.                                                                                                                 |
| `promotedSuggestion.count`  | Defines the number of autosuggest results with doctype `PROMOTED_SUGGESTION`. Default value: **2**.                                                               |
| `popularProducts.filter`    | Restrict the popular products based on **field name** criteria. Works like the `filter` parameter in Search/Browse API (only for autosuggest `popularProducts`).  |
| `popularProducts.filter-id` | Restrict the popular products based on **field ID** criteria. Works like the `filter-id` parameter in Search/Browse API (only for autosuggest `popularProducts`). |
| `filter`                    | Restrict the products based on criteria passed using **field-name**.                                                                                              |
| `spellcheck`                | Enables spellcheck in autosuggest. When `spellcheck=true`, a **did-you-mean** block is returned (default: **false**).                                             |
| `version`                   | **Mandatory.** Version of the API. Only **V2** is supported as **V1 is deprecated**.                                                                              |
| `variants`                  | Enables or disables variants in the API response. Default value: **false**.                                                                                       |

> 📘 NOTE
>
> To read more about the aforementioned parameters, refer Search API.

**Response Parameters**\
Unbxd returns the list of products which match the search criteria. The response would be in application/json or application/xml content type format.

The table below describes the different response keys of an autosuggest call.

| **Attribute Name**      | **Type** | **Description**                                                                                                                                 |
| ----------------------- | -------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| `autosuggest`           | String   | The query string suggested by Unbxd for the autosuggest                                                                                         |
| `doctype`               | Enum     | The type of autosuggest. Possible values: `POPULAR_PRODUCTS`, `TOP_SEARCH_QUERIES`, `PROMOTED_SUGGESTION`, `IN_FIELD`, `KEYWORD_SUGGESTION`     |
| `unbxdAutosuggestSrc`   | String   | The field on which the autosuggest string was generated (present only for `IN_FIELD` doctype results)                                           |
| `unbxdAutosuggestScore` | Float    | The relevancy score given to the autosuggest string by Unbxd (not meant for client-side use)                                                    |
| `uniqueId`              | String   | Random ID for each autosuggest string. For popular products, the format is `popularProduct_<PRODUCT_ID>`                                        |
| `_in`                   | List     | Fields ending with `_in` are present for `IN_FIELD` doctype. E.g., `brand_in` contains all possible values of `brand` linked to the autosuggest |
| `price`                 | Decimal  | Price of the suggested product (only applicable for popular products)                                                                           |
| `imageUrl`              | Link     | URL of the product’s thumbnail image (only for popular products)                                                                                |
| `productUrl`            | Link     | URL of the suggested product page (only for popular products)                                                                                   |