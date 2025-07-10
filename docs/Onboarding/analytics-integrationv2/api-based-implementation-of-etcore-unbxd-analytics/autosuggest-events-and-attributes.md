---
title: Autosuggest Events and Attributes
deprecated: false
hidden: false
metadata:
  robots: index
---
## IN\_FIELD

Template API:

```
https://tracker.unbxdapi.com/v2/1p.jpg
?data={"query":"{{suggested-query}}",
"autosuggest_data":{"autosuggest_type":"IN_FIELD",
"autosuggest_suggestion":"{{suggested-query}}",
"field_value":”value”,
"field_name":”categoryPath1”,
"unbxdprank":”2”,"internal_query":"{{original-query}}"},
"url":"{{url-of-the-website}}","referrer":”{{reference-link}}”,
"visit_type":"{{first_or_repeat}}",
"visitId":"{{visit-id}}"}
&UnbxdKey={{unbxd-sitekey}}
&action=search
&uid={{uid}}
&t=1666830840426|0.12139712486982823

```

Refer here for our [sample API](\[https://tracker.unbxdapi.com/v2/1p.jpg?data=%7B%22query%22%3A%22Drake%7CDrake%22%2C%22autosuggest_data%22%3A%7B%22autosuggest_type%22%3A%22IN_FIELD%22%2C%22autosuggest_suggestion%22%3A%22Drake%7CDrake%22%2C%22field_name%22%3A%22categoryURLMapping_in%22%2C%22field_value%22%3A%22Drake%7CDrake%22%2C%22src_field%22%3A%22%22%2C%22internal_query%22%3A%22%22%7D%2C%22url%22%3A%22https%3A//www.demp.unbxd.com.com.au/c/Sofas%3Fredirectq%3Dsofas%22%2C%22referrer%22%3A%22https%3A//www.demo.unbxd.com.au/search/Sofas%22%2C%22visit_type%22%3A%22repeat%22%2C%22ver%22%3A%224.0.28%22%2C%22_uf%22%3A3902881952%2C%22visitId%22%3A%22visitId-1709116400821-5910%22%7D\&UnbxdKey=demo-unbxd700181503576558\&action=search\&uid=uid-1707194142543-92694\&t=1709118278254%7C0.2816574258470903]\(https://tracker.unbxdapi.com/v2/1p.jpg?data=%7B%22query%22%3A%22Drake%7CDrake%22%2C%22autosuggest_data%22%3A%7B%22autosuggest_type%22%3A%22IN_FIELD%22%2C%22autosuggest_suggestion%22%3A%22Drake%7CDrake%22%2C%22field_name%22%3A%22categoryURLMapping_in%22%2C%22field_value%22%3A%22Drake%7CDrake%22%2C%22src_field%22%3A%22%22%2C%22internal_query%22%3A%22%22%7D%2C%22url%22%3A%22https%3A//www.demp.unbxd.com.com.au/c/Sofas%3Fredirectq%3Dsofas%22%2C%22referrer%22%3A%22https%3A//www.demo.unbxd.com.au/search/Sofas%22%2C%22visit_type%22%3A%22repeat%22%2C%22ver%22%3A%224.0.28%22%2C%22_uf%22%3A3902881952%2C%22visitId%22%3A%22visitId-1709116400821-5910%22%7D\&UnbxdKey=demo-unbxd700181503576558\&action=search\&uid=uid-1707194142543-92694\&t=1709118278254%7C0.2816574258470903\))

Payload details:

| **Attribute Name**       | **Type** | **Value to Pass**                                                                                                                            |                                                                 |                      |
| :----------------------- | :------- | :------------------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------- | :------------------- |
| `query`                  | `string` | Suggested query                                                                                                                              |                                                                 |                      |
| `autosuggest_type`       | `string` | `IN_FIELD` autosuggest type selected and submitted for search, usually the same as the value of the `doctype` field in Unbxd autosuggest API |                                                                 |                      |
| `autosuggest_suggestion` | `string` | Suggested query in Infield                                                                                                                   |                                                                 |                      |
| `field_name`             | `string` | The name of the field used for the `IN_FIELD` suggestion                                                                                     |                                                                 |                      |
| `field_value`            | `string` | The value of the field in the suggestion                                                                                                     |                                                                 |                      |
| `unbxdprank`             | `string` | Rank of the product from the overall list of suggestions                                                                                     |                                                                 |                      |
| `internal_query`         | `string` | The typed query (the current search string prefix) in the search box, which led to the suggestions in autosuggest                            |                                                                 |                      |
| `url`                    | `string` | Website URL where the search is performed                                                                                                    |                                                                 |                      |
| `visit_type`             | `string` | Either `"first_time"` or `"repeat"`                                                                                                          |                                                                 |                      |
| `UnbxdKey`               | `string` | UnbxdSitekey value                                                                                                                           |                                                                 |                      |
| `uid`                    | `string` | `unbxd.userId` (Needs to be extracted from the cookie)                                                                                       |                                                                 |                      |
| `t`                      | `string` | Timestamp formula: \`t : current\_time \\                                                                                                    | random number between 0 to 1`and`t = new Date().getTime() + ‘\\ | ’ + Math.random();\` |
| `referrer`               | `string` | Link from where the page is opened \`referrer: sessionStorage.getItem('urlPrevious') \\                                                      | \| document.referrer \\                                         | \| '';\`             |

## POPULAR\_PRODUCTS

Template API:

```
https://tracker.unbxdapi.com/v2/1p.jpg
?data={"pid":"{{uniqueId-of-the-product}}",
"qty":"{{quantity-selected}}",
"price":"{{unit-price-for-product}}",
"url":"{{url-of-the-website}}",
"referrer":”{{reference-link}}”,
"visit_type":"{{first_or_repeat}}",
"visitId":"{{visit-id}}"}
&UnbxdKey={{unbxd-sitekey}}
&action=order
&uid={{uid}}1658904085468-92302
&t=1662367087116|0.07798836811209986

```

Refer here for our [sample API](\[https://tracker.unbxdapi.com/v2/1p.jpg?data=%7B%22products%22%3A%5B%7B%22pid%22%3A%229500%22%2C%22qty%22%3A%221%22%2C%22price%22%3A%22153%22%2C%22variantId%22%3A%22V96576%22%7D%2C%7B%22pid%22%3A%229501%22%2C%22qty%22%3A%222%22%2C%22price%22%3A%22143%22%2C%22variantId%22%3A%22V980560%22%7D%2C%7B%22pid%22%3A%229502%22%2C%22qty%22%3A%225%22%2C%22price%22%3A%22133%22%2C%22variantId%22%3A%22V980033%22%7D%5D%2C%22url%22%3A%22http%3A%2F%2Flocalhost%3A8080%2F%22%2C%22referrer%22%3A%22%22%2C%22visit_type%22%3A%22repeat%22%2C%22ver%22%3A%224.0.28%22%2C%22_uf%22%3A4213677804%2C%22visitId%22%3A%22visitId-1679387024735-20128%22%7D\&UnbxdKey=demo-unbxd700181503576558\&action=order\&uid=uid-1653404599885-19305\&t=1679387036973%7C0.7978658173524473]\(https://tracker.unbxdapi.com/v2/1p.jpg?data=%7B%22products%22%3A%5B%7B%22pid%22%3A%229500%22%2C%22qty%22%3A%221%22%2C%22price%22%3A%22153%22%2C%22variantId%22%3A%22V96576%22%7D%2C%7B%22pid%22%3A%229501%22%2C%22qty%22%3A%222%22%2C%22price%22%3A%22143%22%2C%22variantId%22%3A%22V980560%22%7D%2C%7B%22pid%22%3A%229502%22%2C%22qty%22%3A%225%22%2C%22price%22%3A%22133%22%2C%22variantId%22%3A%22V980033%22%7D%5D%2C%22url%22%3A%22http%3A%2F%2Flocalhost%3A8080%2F%22%2C%22referrer%22%3A%22%22%2C%22visit_type%22%3A%22repeat%22%2C%22ver%22%3A%224.0.28%22%2C%22_uf%22%3A4213677804%2C%22visitId%22%3A%22visitId-1679387024735-20128%22%7D\&UnbxdKey=demo-unbxd700181503576558\&action=order\&uid=uid-1653404599885-19305\&t=1679387036973%7C0.7978658173524473\))

Payload details:

| **Attribute Name** | **Type** | **Value to Pass**                                                                                                                                    |                                                                 |                      |
| :----------------- | :------- | :--------------------------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------- | :------------------- |
| `query`            | `string` | Title of the product                                                                                                                                 |                                                                 |                      |
| `autosuggest_type` | `string` | `POPULAR_PRODUCTS` autosuggest type selected and submitted for search, usually the same as the value of the `doctype` field in Unbxd autosuggest API |                                                                 |                      |
| `pid`              | `string` | Unique id of the product, to be taken from the search API response                                                                                   |                                                                 |                      |
| `field_name`       | `string` | The name of the field used for the `IN_FIELD` suggestion                                                                                             |                                                                 |                      |
| `field_value`      | `string` | The value of the field in the suggestion                                                                                                             |                                                                 |                      |
| `unbxdprank`       | `string` | Rank of the product from the overall list of suggestions                                                                                             |                                                                 |                      |
| `internal_query`   | `string` | The typed query (the current search string prefix) in the search box, which led to the suggestions in autosuggest                                    |                                                                 |                      |
| `url`              | `string` | Website URL where the search is performed                                                                                                            |                                                                 |                      |
| `UnbxdKey`         | `string` | UnbxdSitekey value                                                                                                                                   |                                                                 |                      |
| `uid`              | `string` | `unbxd.userId` (Needs to be extracted from the cookie)                                                                                               |                                                                 |                      |
| `t`                | `string` | Timestamp formula: \`t : current\_time \\                                                                                                            | random number between 0 to 1`and`t = new Date().getTime() + ‘\\ | ’ + Math.random();\` |

The `CLICK` event and `CART` event will be be applicable to `POPULAR_PRODUCTS`.

### CLICK

When a popular product is clicked from the autosuggest widget,

1. Fire the autosuggest `POPULAR_PRODUCTS` event.

2. Retrieve the `pid`.

3. Fire the [click event](/integrations/api-implementation/event-specific-attributes#product-click).

### CART

1. Fire the autosuggest `POPULAR_PRODUCTS` event.

2. Retrieve the `pid`.

3. Fire the [click event](/integrations/api-implementation/event-specific-attributes#product-click).

4. After firing the click event, fire the [add to cart event](/integrations/api-implementation/event-specific-attributes#add-to-cart).

## KEYWORD\_SUGGESTION

Template API:

```
https://tracker.unbxdapi.com/v2/1p.jpg
?data={"query":"{{suggested-query}}",
"autosuggest_data":{"autosuggest_type":"KEYWORD_SUGGESTION","autosuggest_suggestion":"{{suggested-query}}",
"unbxdprank":"{{rank-of-product}}",
"internal_query":"{{original-query}}"},
"url":"{{url-of-the-website}}",
"referrer":”{{reference-link}}”,
"visit_type":"{{first_or_repeat}}",
"visitId":"{{visit-id}}"}
&UnbxdKey={{unbxd-sitekey}}
&action=search
&uid={{uid}}
&t=1666830840426|0.12139712486982823

```

Refer here for our [sample API](\[https://tracker.unbxdapi.com/v2/1p.jpg?data=%7B%22query%22%3A%22Sofa%20Set%22%2C%22autosuggest_data%22%3A%7B%22autosuggest_type%22%3A%22KEYWORD_SUGGESTION%22%2C%22autosuggest_suggestion%22%3A%22Sofa%20Set%22%2C%22field_name%22%3A%22autosuggest%22%2C%22field_value%22%3A%22Sofa%20Set%22%2C%22src_field%22%3A%22%22%2C%22internal_query%22%3A%22sofas%22%7D%2C%22url%22%3A%22https%3A//www.demo.unbxd.com.au/search/2%2520Seater%2520Sofa%22%2C%22referrer%22%3A%22https%3A//www.demo.unbxd.com.au/c/Drake%22%2C%22visit_type%22%3A%22repeat%22%2C%22ver%22%3A%224.0.28%22%2C%22_uf%22%3A3902881952%2C%22visitId%22%3A%22visitId-1709116400821-5910%22%7D\&UnbxdKey=demo-unbxd700181503576558\&action=search\&uid=uid-1707194142543-92694\&t=1709118365818%7C0.17527713761166375]\(https://tracker.unbxdapi.com/v2/1p.jpg?data=%7B%22query%22%3A%22Sofa%20Set%22%2C%22autosuggest_data%22%3A%7B%22autosuggest_type%22%3A%22KEYWORD_SUGGESTION%22%2C%22autosuggest_suggestion%22%3A%22Sofa%20Set%22%2C%22field_name%22%3A%22autosuggest%22%2C%22field_value%22%3A%22Sofa%20Set%22%2C%22src_field%22%3A%22%22%2C%22internal_query%22%3A%22sofas%22%7D%2C%22url%22%3A%22https%3A//www.demo.unbxd.com.au/search/2%2520Seater%2520Sofa%22%2C%22referrer%22%3A%22https%3A//www.demo.unbxd.com.au/c/Drake%22%2C%22visit_type%22%3A%22repeat%22%2C%22ver%22%3A%224.0.28%22%2C%22_uf%22%3A3902881952%2C%22visitId%22%3A%22visitId-1709116400821-5910%22%7D\&UnbxdKey=demo-unbxd700181503576558\&action=search\&uid=uid-1707194142543-92694\&t=1709118365818%7C0.17527713761166375\))

Payload details:

| **Attribute Name**       | **Type** | **Value to Pass**                                                                                                                                      |                                                                 |                      |
| :----------------------- | :------- | :----------------------------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------- | :------------------- |
| `query`                  | `string` | Suggested query in keywords                                                                                                                            |                                                                 |                      |
| `autosuggest_type`       | `string` | `KEYWORD_SUGGESTION` autosuggest type selected and submitted for search, usually the same as the value of the `doctype` field in Unbxd autosuggest API |                                                                 |                      |
| `autosuggest_suggestion` | `string` | Suggested query in Infield                                                                                                                             |                                                                 |                      |
| `unbxdprank`             | `string` | Rank of the product from the overall list of suggestions                                                                                               |                                                                 |                      |
| `internal_query`         | `string` | The typed query (the current search string prefix) in the search box, which led to the suggestions in autosuggest                                      |                                                                 |                      |
| `url`                    | `string` | Website URL where the search is performed                                                                                                              |                                                                 |                      |
| `UnbxdKey`               | `string` | UnbxdSitekey value                                                                                                                                     |                                                                 |                      |
| `uid`                    | `string` | `unbxd.userId` (Needs to be extracted from the cookie)                                                                                                 |                                                                 |                      |
| `t`                      | `string` | Timestamp formula: \`t : current\_time \\                                                                                                              | random number between 0 to 1`and`t = new Date().getTime() + ‘\\ | ’ + Math.random();\` |
| `referrer`               | `string` | Link from where the page is opened \`referrer: sessionStorage.getItem('urlPrevious') \\                                                                | \| document.referrer \\                                         | \| '';\`             |

## TOP\_SEARCH\_QUERIES

Template API:

```
https://tracker.unbxdapi.com/v2/1p.jpg
?data={"query":"{{suggested-query}}",
"autosuggest_data":{"autosuggest_type":"TOP_SEARCH_QUERIES",
"autosuggest_suggestion":"{{suggested-query}}",
"unbxdprank":"{{rank-of-product}}",
"internal_query":"{{original-query}}"},
"url":"{{url-of-the-website}}",
"referrer":”{{reference-link}}”,
"visit_type":"{{first_or_repeat}}",
"visitId":"{{visit-id}}"}
&UnbxdKey={{unbxd-sitekey}}
&action=search
&uid={{uid}}
&t=1666851030913|0.2127782620243308

```

Refer here for our [sample API](\[https://tracker.unbxdapi.com/v2/1p.jpg?data=%7B%22query%22%3A%222%20Seater%20Sofa%22%2C%22autosuggest_data%22%3A%7B%22autosuggest_type%22%3A%22TOP_SEARCH_QUERIES%22%2C%22autosuggest_suggestion%22%3A%222%20Seater%20Sofa%22%2C%22field_name%22%3A%22autosuggest%22%2C%22field_value%22%3A%222%20Seater%20Sofa%22%2C%22src_field%22%3A%22%22%2C%22internal_query%22%3A%22sofa%22%7D%2C%22url%22%3A%22https%3A//www.demo.unbxd.com.au/c/Drake%22%2C%22referrer%22%3A%22https%3A//www.demo.unbxd.com.au/c/Sofas%3Fredirectq%3Dsofas%22%2C%22visit_type%22%3A%22repeat%22%2C%22ver%22%3A%224.0.28%22%2C%22_uf%22%3A3902881952%2C%22visitId%22%3A%22visitId-1709116400821-5910%22%7D\&UnbxdKey=demo-unbxd700181503576558\&action=search\&uid=uid-1707194142543-92694\&t=1709118321269%7C0.4497925431675631]\(https://tracker.unbxdapi.com/v2/1p.jpg?data=%7B%22query%22%3A%222%20Seater%20Sofa%22%2C%22autosuggest_data%22%3A%7B%22autosuggest_type%22%3A%22TOP_SEARCH_QUERIES%22%2C%22autosuggest_suggestion%22%3A%222%20Seater%20Sofa%22%2C%22field_name%22%3A%22autosuggest%22%2C%22field_value%22%3A%222%20Seater%20Sofa%22%2C%22src_field%22%3A%22%22%2C%22internal_query%22%3A%22sofa%22%7D%2C%22url%22%3A%22https%3A//www.demo.unbxd.com.au/c/Drake%22%2C%22referrer%22%3A%22https%3A//www.demo.unbxd.com.au/c/Sofas%3Fredirectq%3Dsofas%22%2C%22visit_type%22%3A%22repeat%22%2C%22ver%22%3A%224.0.28%22%2C%22_uf%22%3A3902881952%2C%22visitId%22%3A%22visitId-1709116400821-5910%22%7D\&UnbxdKey=demo-unbxd700181503576558\&action=search\&uid=uid-1707194142543-92694\&t=1709118321269%7C0.4497925431675631\))

Payload details:

| **Attribute Name**       | **Type** | **Value to Pass**                                                                                                                                      |                                                                 |                      |
| :----------------------- | :------- | :----------------------------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------- | :------------------- |
| `query`                  | `string` | Suggested query                                                                                                                                        |                                                                 |                      |
| `autosuggest_type`       | `string` | `TOP_SEARCH_QUERIES` autosuggest type selected and submitted for search, usually the same as the value of the `doctype` field in Unbxd autosuggest API |                                                                 |                      |
| `autosuggest_suggestion` | `string` | Suggested query in Infield                                                                                                                             |                                                                 |                      |
| `unbxdprank`             | `string` | Rank of the product from the overall list of suggestions                                                                                               |                                                                 |                      |
| `internal_query`         | `string` | The typed query (the current search string prefix) in the search box, which led to the suggestions in autosuggest                                      |                                                                 |                      |
| `url`                    | `string` | Website URL where the search is performed                                                                                                              |                                                                 |                      |
| `UnbxdKey`               | `string` | UnbxdSitekey value                                                                                                                                     |                                                                 |                      |
| `uid`                    | `string` | `unbxd.userId` (Needs to be extracted from the cookie)                                                                                                 |                                                                 |                      |
| `t`                      | `string` | Timestamp formula: \`t : current\_time \\                                                                                                              | random number between 0 to 1`and`t = new Date().getTime() + ‘\\ | ’ + Math.random();\` |
| `referrer`               | `string` | Link from where the page is opened \`referrer: sessionStorage.getItem('urlPrevious') \\                                                                | \| document.referrer \\                                         | \| '';\`             |

## POPULAR\_PRODUCTS\_FILTERED

Template API:

```
https://tracker.unbxdapi.com/v2/1p.jpg
?data={"query":"{{suggested-query}}",
"autosuggest_data":{"autosuggest_type":"POPULAR_PRODUCTS_FILTERED",
"autosuggest_suggestion":"{{suggested-query}}",
"unbxdprank":"{{rank-of-product}}",
"internal_query":"{{original-query}}"},
"url":"{{url-of-the-website}}",
"referrer":”{{reference-link}}”,
"visit_type":"{{first_or_repeat}}",
"visitId":"{{visit-id}}"}
&UnbxdKey={{unbxd-sitekey}}
&action=search
&uid={{uid}}
&t=1666851030913|0.2127782620243308

```

Refer here for our [sample API](\[https://tracker.unbxdapi.com/v2/1p.jpg?data=%7B%22query%22%3A%22Kenza%203%20Seater%20Sofa%20Bed%22%2C%22autosuggest_data%22%3A%7B%22autosuggest_type%22%3A%22POPULAR_PRODUCTS%22%2C%22pid%22%3A%22BNC_KEASBOOOLI%22%2C%22unbxdprank%22%3A1%2C%22internal_query%22%3A%22red%20sofa%22%7D%2C%22url%22%3A%22https%3A//www.demo.unbxd.com.au/Categories/Storage-%26-Office/Office/Makeup-Desks/c/makeup-desks%22%2C%22referrer%22%3A%22https%3A//www.demo.unbxd.com.au/Categories/Bedroom-%26-Mattresses/Beds/Sofa-Beds-%26-Futons/Kenza-3-Seater-Sofa-Bed/p/KEASBD3STOOOLINBLK%22%2C%22visit_type%22%3A%22repeat%22%2C%22ver%22%3A%224.0.28%22%2C%22_uf%22%3A3902881952%2C%22visitId%22%3A%22visitId-1709116400821-5910%22%7D\&UnbxdKey=demo-unbxd700181503576558\&action=search\&uid=uid-1707194142543-92694\&t=1709118176112%7C0.7945598269101375]\(https://tracker.unbxdapi.com/v2/1p.jpg?data=%7B%22query%22%3A%22Kenza%203%20Seater%20Sofa%20Bed%22%2C%22autosuggest_data%22%3A%7B%22autosuggest_type%22%3A%22POPULAR_PRODUCTS%22%2C%22pid%22%3A%22BNC_KEASBOOOLI%22%2C%22unbxdprank%22%3A1%2C%22internal_query%22%3A%22red%20sofa%22%7D%2C%22url%22%3A%22https%3A//www.demo.unbxd.com.au/Categories/Storage-%26-Office/Office/Makeup-Desks/c/makeup-desks%22%2C%22referrer%22%3A%22https%3A//www.demo.unbxd.com.au/Categories/Bedroom-%26-Mattresses/Beds/Sofa-Beds-%26-Futons/Kenza-3-Seater-Sofa-Bed/p/KEASBD3STOOOLINBLK%22%2C%22visit_type%22%3A%22repeat%22%2C%22ver%22%3A%224.0.28%22%2C%22_uf%22%3A3902881952%2C%22visitId%22%3A%22visitId-1709116400821-5910%22%7D\&UnbxdKey=demo-unbxd700181503576558\&action=search\&uid=uid-1707194142543-92694\&t=1709118176112%7C0.7945598269101375\))

Payload details:

| **Attribute Name** | **Type** | **Value to Pass**                                                                                                                                             |                                                                 |                      |
| :----------------- | :------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------ | :-------------------------------------------------------------- | :------------------- |
| `query`            | `string` | Title of the product                                                                                                                                          |                                                                 |                      |
| `autosuggest_type` | `string` | `POPULAR_PRODUCTS_FILTERED` autosuggest type selected and submitted for search, usually the same as the value of the `doctype` field in Unbxd autosuggest API |                                                                 |                      |
| `pid`              | `string` | Unique id of the product, to be taken from the search API response                                                                                            |                                                                 |                      |
| `unbxdprank`       | `string` | Rank of the product from the overall list of suggestions                                                                                                      |                                                                 |                      |
| `internal_query`   | `string` | The typed query (the current search string prefix) in the search box, which led to the suggestions in autosuggest                                             |                                                                 |                      |
| `url`              | `string` | Website URL where the search is performed                                                                                                                     |                                                                 |                      |
| `UnbxdKey`         | `string` | UnbxdSitekey value                                                                                                                                            |                                                                 |                      |
| `uid`              | `string` | `unbxd.userId` (Needs to be extracted from the cookie)                                                                                                        |                                                                 |                      |
| `t`                | `string` | Timestamp formula: \`t : current\_time \\                                                                                                                     | random number between 0 to 1`and`t = new Date().getTime() + ‘\\ | ’ + Math.random();\` |
| `referrer`         | `string` | Link from where the page is opened \`referrer: sessionStorage.getItem('urlPrevious') \\                                                                       | \| document.referrer \\                                         | \| '';\`             |

## PROMOTED\_SUGGESTION

Template API:

```
https://tracker.unbxdapi.com/v2/1p.jpg
?data={"query":"{{suggested-query}}",
"autosuggest_data":{"autosuggest_type":"PROMOTED_SUGGESTION",
"autosuggest_suggestion":"{{suggested-query}}",
"unbxdprank":"{{rank-of-product}}",
"internal_query":"{{original-query}}"},
"url":"{{url-of-the-website}}",
"referrer":”{{reference-link}}”,
"visit_type":"{{first_or_repeat}}",
"visitId":"{{visit-id}}"}
&UnbxdKey={{unbxd-sitekey}}
&action=search
&uid={{uid}}
&t=1666851030913|0.2127782620243308

```

Refer here for our [sample API](\[https://tracker.unbxdapi.com/v2/1p.jpg?data=%7B%22query%22%3A%22Sofas%22%2C%22autosuggest_data%22%3A%7B%22autosuggest_type%22%3A%22PROMOTED_SUGGESTION%22%2C%22autosuggest_suggestion%22%3A%22Sofas%22%2C%22field_name%22%3A%22autosuggest%22%2C%22field_value%22%3A%22Sofas%22%2C%22src_field%22%3A%22%22%2C%22internal_query%22%3A%22sof%22%7D%2C%22url%22%3A%22https%3A//www.demo.unbxd.com.au/Categories/Bedroom-%252526-Mattresses/Beds/Sofa-Beds-%252526-Futons/Kenza-3-Seater-Sofa-Bed/p/KEASBD3STOOOLINRED%22%2C%22referrer%22%3A%22https%3A//www.demo.unbxd.com.au/Categories/Storage-%26-Office/Office/Makeup-Desks/c/makeup-desks%22%2C%22visit_type%22%3A%22repeat%22%2C%22ver%22%3A%224.0.28%22%2C%22_uf%22%3A3902881952%2C%22visitId%22%3A%22visitId-1709116400821-5910%22%7D\&UnbxdKey=demo-unbxd700181503576558\&action=search\&uid=uid-1707194142543-92694\&t=1709118207606%7C0.058123470392127174]\(https://tracker.unbxdapi.com/v2/1p.jpg?data=%7B%22query%22%3A%22Sofas%22%2C%22autosuggest_data%22%3A%7B%22autosuggest_type%22%3A%22PROMOTED_SUGGESTION%22%2C%22autosuggest_suggestion%22%3A%22Sofas%22%2C%22field_name%22%3A%22autosuggest%22%2C%22field_value%22%3A%22Sofas%22%2C%22src_field%22%3A%22%22%2C%22internal_query%22%3A%22sof%22%7D%2C%22url%22%3A%22https%3A//www.demo.unbxd.com.au/Categories/Bedroom-%252526-Mattresses/Beds/Sofa-Beds-%252526-Futons/Kenza-3-Seater-Sofa-Bed/p/KEASBD3STOOOLINRED%22%2C%22referrer%22%3A%22https%3A//www.demo.unbxd.com.au/Categories/Storage-%26-Office/Office/Makeup-Desks/c/makeup-desks%22%2C%22visit_type%22%3A%22repeat%22%2C%22ver%22%3A%224.0.28%22%2C%22_uf%22%3A3902881952%2C%22visitId%22%3A%22visitId-1709116400821-5910%22%7D\&UnbxdKey=demo-unbxd700181503576558\&action=search\&uid=uid-1707194142543-92694\&t=1709118207606%7C0.058123470392127174\))

Payload details:

| **Attribute Name**       | **Type** | **Value to Pass**                                                                                                                                       |                                                                 |                      |
| :----------------------- | :------- | :------------------------------------------------------------------------------------------------------------------------------------------------------ | :-------------------------------------------------------------- | :------------------- |
| `query`                  | `string` | Suggested query                                                                                                                                         |                                                                 |                      |
| `autosuggest_type`       | `string` | `PROMOTED_SUGGESTION` autosuggest type selected and submitted for search, usually the same as the value of the `doctype` field in Unbxd autosuggest API |                                                                 |                      |
| `autosuggest_suggestion` | `string` | Suggested query in Infield                                                                                                                              |                                                                 |                      |
| `unbxdprank`             | `string` | Rank of the product from the overall list of suggestions                                                                                                |                                                                 |                      |
| `internal_query`         | `string` | The typed query (the current search string prefix) in the search box, which led to the suggestions in autosuggest                                       |                                                                 |                      |
| `url`                    | `string` | Website URL where the search is performed                                                                                                               |                                                                 |                      |
| `UnbxdKey`               | `string` | UnbxdSitekey value                                                                                                                                      |                                                                 |                      |
| `uid`                    | `string` | `unbxd.userId` (Needs to be extracted from the cookie)                                                                                                  |                                                                 |                      |
| `t`                      | `string` | Timestamp formula: \`t : current\_time \\                                                                                                               | random number between 0 to 1`and`t = new Date().getTime() + ‘\\ | ’ + Math.random();\` |
| `referrer`               | `string` | Link from where the page is opened \`referrer: sessionStorage.getItem('urlPrevious') \\                                                                 | \| document.referrer \\                                         | \| '';\`             |

## FIELD\_TYPE\_SUGGESTION

Template API:

```
https://tracker.unbxdapi.com/v2/1p.jpg
?data={"query":"{{suggested-query}}",
"autosuggest_data":{"autosuggest_type":"KEYWORD_SUGGESTION",
"autosuggest_suggestion":"{{suggested-query}}",
"unbxdprank":"{{rank-of-product}}",
"internal_query":"{{original-query}}"},
"url":"{{url-of-the-website}}",
"referrer":”{{reference-link}}”,
"visit_type":"{{first_or_repeat}}",
"visitId":"{{visit-id}}"}
&UnbxdKey={{unbxd-sitekey}}
&action=search
&uid={{uid}}
&t=1666851030913|0.2127782620243308
&misc:{“unxAsType”:”FIELD_TYPE_SUGGESTION”,”unxAsFieldName”:”categoryPath1”}

```

Payload details:

| **Attribute Name**       | **Type** | **Value to Pass**                                                                                                                                      |                                                                 |                      |
| :----------------------- | :------- | :----------------------------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------- | :------------------- |
| `query`                  | `string` | Suggested query                                                                                                                                        |                                                                 |                      |
| `autosuggest_type`       | `string` | `KEYWORD_SUGGESTION` autosuggest type selected and submitted for search, usually the same as the value of the `doctype` field in Unbxd autosuggest API |                                                                 |                      |
| `autosuggest_suggestion` | `string` | Suggested query in Infield                                                                                                                             |                                                                 |                      |
| `unbxdprank`             | `string` | Rank of the product from the overall list of suggestions                                                                                               |                                                                 |                      |
| `internal_query`         | `string` | The typed query (the current search string prefix) in the search box, which led to the suggestions in autosuggest                                      |                                                                 |                      |
| `url`                    | `string` | Website URL where the search is performed                                                                                                              |                                                                 |                      |
| `UnbxdKey`               | `string` | UnbxdSitekey value                                                                                                                                     |                                                                 |                      |
| `uid`                    | `string` | `unbxd.userId` (Needs to be extracted from the cookie)                                                                                                 |                                                                 |                      |
| `t`                      | `string` | Timestamp formula: \`t : current\_time \\                                                                                                              | random number between 0 to 1`and`t = new Date().getTime() + ‘\\ | ’ + Math.random();\` |
| `referrer`               | `string` | Link from where the page is opened \`referrer: sessionStorage.getItem('urlPrevious') \\                                                                | \| document.referrer \\                                         | \| '';\`             |

In addition to the attributes mentioned above, some MANDATORY miscellaneous data must also be included. These should be added under the object named `misc`. Please refer to the table below for the specific attributes to be added under misc.

| **Attribute Name** | **Type** | **Value to Pass**                                                                                                                                                             |
| ------------------ | -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `unxAsType`        | `string` | This attribute goes into the `misc` object to indicate this is a type of `FIELD_TYPE_SUGGESTION`.                                                                             |
| `unxAsFieldName`   | `string` | This attribute goes into the `misc` object to indicate the `field` on which the `FIELD_TYPE_SUGGESTION` has been set up. Here, the value can be the field name from the feed. |

Example schema (showcasing only a part of the api): `&misc:{“unxAsType”:”FIELD_TYPE_SUGGESTION”,”unxAsFieldName”:”categoryPath1”}`

## TRENDING\_QUERIES

Template API:

```
https://tracker.unbxdapi.com/v2/1p.jpg
?data={"query":"{{suggested-query}}",
"autosuggest_data":{"autosuggest_type":"TOP_SEARCH_QUERIES",
"autosuggest_suggestion":"{{suggested-query}}",
"pid":"{{uniqueId-of-the-product}}",
"unbxdprank":"{{rank-of-product}}",
"internal_query":"{{original-query}}"},
"url":"{{url-of-the-website}}",
"referrer":”{{reference-link}}”,
"visit_type":"{{first_or_repeat}}",
"visitId":"{{visit-id}}"}
&UnbxdKey={{unbxd-sitekey}}
&action=search
&uid={{uid}}
&t=1666851030913|0.2127782620243308
&misc:{“unxAsType”:”TRENDING_QUERIES”}

```

Payload details:

| **Attribute Name**       | **Type** | **Value to Pass**                                                                                                                                      |                                                                 |                      |
| :----------------------- | :------- | :----------------------------------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------- | :------------------- |
| `query`                  | `string` | Suggested query in Infield                                                                                                                             |                                                                 |                      |
| `autosuggest_type`       | `string` | `TOP_SEARCH_QUERIES` autosuggest type selected and submitted for search, usually the same as the value of the `doctype` field in Unbxd autosuggest API |                                                                 |                      |
| `autosuggest_suggestion` | `string` | Suggested query in Infield                                                                                                                             |                                                                 |                      |
| `unbxdprank`             | `string` | Rank of the product from the overall list of suggestions                                                                                               |                                                                 |                      |
| `internal_query`         | `string` | The typed query (the current search string prefix) in the search box, which led to the suggestions in autosuggest                                      |                                                                 |                      |
| `url`                    | `string` | Website URL where the search is performed                                                                                                              |                                                                 |                      |
| `UnbxdKey`               | `string` | UnbxdSitekey value                                                                                                                                     |                                                                 |                      |
| `uid`                    | `string` | `unbxd.userId` (Needs to be extracted from the cookie)                                                                                                 |                                                                 |                      |
| `t`                      | `string` | Timestamp formula: \`t : current\_time \\                                                                                                              | random number between 0 to 1`and`t = new Date().getTime() + ‘\\ | ’ + Math.random();\` |
| `referrer`               | `string` | Link from where the page is opened \`referrer: sessionStorage.getItem('urlPrevious') \\                                                                | \| document.referrer \\                                         | \| '';\`             |

In addition to the attributes mentioned above, some MANDATORY miscellaneous data must also be included. These should be added under the object named `misc`. Please refer to the table below for the specific attributes to be added under misc.\
Example schema (showcasing only a part of the api): `&misc:{“unxAsType”:”TRENDING_QUERIES”}`

| **Attribute Name** | **Type** | **Value to Pass**                                                                            |
| ------------------ | -------- | -------------------------------------------------------------------------------------------- |
| `unxAsType`        | `string` | This attribute goes into the `misc` object to indicate this is a type of `TRENDING_QUERIES`. |